AdBlock filters for ***sing-box***, generated based on https://raw.githubusercontent.com/217heidai/adblockfilters/refs/heads/main/rules/AdGuard_DNS_filter.txt

Steps to make this files:
1. ```curl https://raw.githubusercontent.com/217heidai/adblockfilters/refs/heads/main/rules/AdGuard_DNS_filter.txt > AdGuard_DNS_filter.txt```

2. ```jq -Rs 'split("\n")|map(select(startswith("||")))|map(sub("^\\|\\|";"")|sub("\\^$";""))|{version:3,rules:[{domain_suffix:.}]}' AdGuard_DNS_filter.txt > blocklist.json```

3. ```jq -Rs 'split("\n")|map(select(startswith("@@||")))|map(sub("^\\@\\@\\|\\|";"")|sub("\\^$";"")|sub("\\^\\|$";""))|{version:3,rules:[{domain_suffix:.}]}' AdGuard_DNS_filter.txt > exceptions.json```

4. ```sing-box rule-set compile --output blocklist.srs blocklist.json```

5. ```sing-box rule-set compile --output exceptions.srs exceptions.json```
