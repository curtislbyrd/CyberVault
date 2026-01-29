# Hunting Cryptocurrency Miners in Splunk

This guide provides effective Splunk searches to detect cryptominers (especially XMRig-style Monero miners).


Prioritize these data sources if you have them:
- Sysmon (EventCode 1, 6, 11)
- Perfmon / CPU metrics
- Process creation logs
- DNS / network / proxy logs

## 1. High / Sustained CPU Usage

High CPU processes (Perfmon style)

    index=* sourcetype=Perfmon* OR sourcetype=cpu OR "CPU" 
    process_cpu_used_percent > 80 
    | stats avg(process_cpu_used_percent) as avg_cpu values(process_name) as processes by host 
    | where avg_cpu > 80 
    | sort - avg_cpu

Top CPU-consuming processes over time

    index=* sourcetype=*process* OR sourcetype=sysmon EventCode=1 
    | timechart span=5m avg(CPU_Percent) by process_name 
    | where avg(CPU_Percent) > 90

## 2. Miner Process Names & Command Lines

Broad keyword search

    index=* ("xmrig" OR xmr OR "stratum+" OR "pool." OR monero OR moneroocean OR "minexmr" OR nanopool OR "nicehash" OR minergate OR cpuminer OR " --donate" OR " --cpu" OR " --algo=rx/0" OR " --threads" OR " --max-cpu-usage")
    | table _time host sourcetype process_name process command_line

Sysmon process creation with suspicious flags

    index=* sourcetype="xmlwineventlog" OR sourcetype=sysmon EventCode=1 
    ("xmrig" OR "stratum+" OR "--algo" OR "--donate-level" OR "--cpu-affinity" OR "pool." OR "monero" OR "xmr")
    | table _time host Computer ProcessId ParentProcessId Image CommandLine

## 3. Network / Mining Pool Connections

DNS queries to mining domains

    index=* sourcetype=dns OR sourcetype=stream:dns 
    (query="*mine*" OR query="*pool*" OR query="*xmr*" OR query="*monero*" OR query="nanopool.org" OR query="minexmr.com" OR query="supportxmr.com" OR query="moneroocean.stream" OR query="nicehash.com" OR query="stratum+tcp")
    | stats count by query host 
    | sort - count

Outbound to common mining ports

    index=* (dest_port=3333 OR dest_port=5555 OR dest_port=7777 OR dest_port=14444 OR dest_port=8080 OR dest_port=443) 
    ("stratum" OR "xmr" OR "monero" OR "pool" OR "mine")
    | table _time src_ip dest_ip dest_port dest_host

Tip: Install the Crypto Firewall app from Splunkbase for known mining IP/domain lookups.

## 4. File / Config Drops

XMRig-related file creation (EventCode 11)

    index=* sourcetype=Sysmon EventCode=11 
    ("config.json" OR "xmrig" OR "WinRing0x64.sys" OR "*.xmr" OR "miner.txt")
    | table _time host TargetFilename ProcessImage

Suspicious driver loads (EventCode 6)

    index=* sourcetype=sysmon EventCode=6 
    ("WinRing0x64.sys" OR "*xmrig*")

## 5. Other Indicators

Browser mining remnants

    index=* sourcetype=*web* OR sourcetype=bro_http 
    ("coinhive" OR "cryptoloot" OR "webmine" OR "authedmine")

Telegram miner droppers

    index=* ("api.telegram.org" OR "t.me" OR "telegram") ("miner" OR "xmrig" OR "download")

Suspicious renamed processes in temp/user paths

    index=* sourcetype=sysmon EventCode=1 
    (Image="*\\Temp\\*" OR Image="*\\AppData\\*" OR Image="*\\ProgramData\\*") 
    ("svchost.exe" OR "conhost.exe" OR "explorer.exe") 
    (ParentImage="*\\powershell*" OR ParentImage="*\\cmd*")

## Quick Hunting Tips
- Start with high CPU → correlate to network + process name/path
- Look for sustained activity (use timechart / streamstats)
- False positives common — require 2–3 signals to investigate
- Sysmon + Perfmon + DNS = strongest combo

Happy hunting!