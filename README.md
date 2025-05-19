import dns.resolver
import sys

# Emoji
dns_emoji = "🌐"
ok = "✅"
fail = "❌"
info = "ℹ️"

record_types = ["A", "AAAA", "MX", "NS", "TXT", "CNAME"]

def query_dns(domain):
    print(f"{dns_emoji} Scansione DNS per: {domain}\n")

    for record in record_types:
        try:
            answers = dns.resolver.resolve(domain, record)
            print(f"{ok} Record {record}:")
            for rdata in answers:
                print(f"  {info} {rdata.to_text()}")
        except Exception:
            print(f"{fail} Nessun record {record} trovato.\n")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(f"{fail} Uso corretto: python dns_scanner.py <dominio>")
        sys.exit(1)

    domain = sys.argv[1]
    query_dns(domain)
