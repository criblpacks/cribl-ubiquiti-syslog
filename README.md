# Cribl Pack for Ubiquiti Unifi
----

This Pack cleans up Ubiquiti Unifi syslog data, normalizing to JSON whenever possible. If an event isn't understood by included parsing rules, trim the excess syslog decorators and pass through. My testing on a live Unifi network with 1 UDMP, 3 APs and several switches saw a reduction of more than 50% of the syslog data, and a dramatic improvement in searchability due to normalizing logs as JSON.

## Requirements Section

Before you begin, ensure that you have met the following requirements:

* Cribl Stream is [installed](https://docs.cribl.io/stream/getting-started-guide/) on a VM/Container/Physical instance near your Unifi gear
    * Alternatively, use a [Cribl Cloud](https://cribl.cloud) instance (free up to 1 TB per day in+out)
* Your Ubiquiti Unifi devices have access to the UDP port on the Stream instance

## Ubiquiti Unifi Configuration

1) In the Unifi controller interface, navigate to System Settings -> Controller Configuration -> Remote Logging
2) Ensure syslog is enabled
3) Enter the name or IP of the Stream instance (or the VIP of the load balancer in front of Stream instances) that will receive syslog 
4) Select the port you will use to to receieve

## Cribl Stream Configuration

1) Install this Pack (Packs -> Add New)
2) Define a syslog Source with the port required (as used above)
3) Create a Route that points your syslog Source in step 2 to this Pack and a destination of your choice
4) In the Pack, under knowledge:
    * `unifi_hosts.csv` should be updated as appropriate for your network
    * `unifi_suppress.csv` contains `appnames` that will be somewhat suppressed
        - Once you have a feel for the data contained in various log message, adjust this file as needed
    * `unifi_matches.csv` defines patterns used to identify fields contained in event data – adjust as needed
5) Optionally, also install the Cribl Syslog Pre-processing Pack from the dispensary to normalize your incoming syslog data

**NOTE**: If you require a load balancer in front of the syslog receiver, you will need to configure it appropriately



## Release Notes

### Version 0.5.1 - 2022-12-08
Renaming to clarify this is for Unifi products, and update verbiage, links

### Version 0.5.0 - 2021-10-25
First general release


## Contributing to the Pack
Feel free to fork the Pack repo and make adjustments. I will review submitted PRs for acceptance and publication. I'm also active in the [Cribl Community Slack](https://cribl.io/community/). Suggestions for enhancements are welcome.


## Contact
To contact: 
- Email `jrust@cribl.io`
- [Cribl Community Slack](https://cribl.io/community/)


## License
[`Apache 2.0`](https://github.com/criblio/appscope/blob/master/LICENSE).
