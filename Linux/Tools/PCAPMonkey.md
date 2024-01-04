A simple git project that uses zeek to parse pcap files and uses ELK + Suricata to display the results in an easier way to visualize the data.

GitHub: https://github.com/certego/PcapMonkey

First is to install [[ELK]] and than download the Open-ET rules for Suricata: `sudo docker compose run --entrypoint='suricata-update -f' suricata`

To analyze pcap files you have to drop them in pcap folder and then run: `sudo docker compose up suricata zeek`

------

- It isn't bad, but I feel like there could be better dashboards and more useful visualizations in Kibana.