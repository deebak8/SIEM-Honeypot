Within Sentinel, create the watchlist:

Name/Alias: geoip
Source type: Local File
Number of lines before row: 0
Search Key: network

Observe the logs now have geographic information, so you can see where the attacks are coming from

let GeoIPDB_FULL = _GetWatchlist("geoip");
let WindowsEvents = SecurityEvent
    | where IpAddress == <attacker IP address>
    | where EventID == 4625
    | order by TimeGenerated desc
    | evaluate ipv4_lookup(GeoIPDB_FULL, IpAddress, network);
WindowsEvents
