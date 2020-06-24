---
layout: page
title: Features & Roadmap \| Amadeus
title1: Features & Roadmap | Amadeus
title2: Features & Roadmap
permalink: /amadeus/features
icon: event
---

Amadeus has deep, pluggable, integration with various file formats, databases and interfaces:

| Data format | [`Source`](https://docs.rs/amadeus/0.2.4/amadeus/trait.Source.html) | [`Destination`](https://docs.rs/amadeus/0.2.4/amadeus/trait.Destination.html) |
|---|---|---|
| CSV | ✔ | ✔ |
| JSON | ✔ | ✔ |
| XML | [👐](https://github.com/constellation-rs/amadeus/issues/15) |  |
| Parquet | ✔ | [🔨](https://github.com/constellation-rs/amadeus) |
| Avro | [🔨](https://github.com/constellation-rs/amadeus) |  |
| PostgreSQL | ✔ | [🔨](https://github.com/constellation-rs/amadeus) |
| HDF5 | [👐](https://github.com/constellation-rs/amadeus) |  |
| Redshift | [👐](https://github.com/constellation-rs/amadeus) |  |
| [CloudFront Logs](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/AccessLogs.html) | ✔ | – |
| [Common Crawl](http://commoncrawl.org/the-data/get-started/) | ✔ | – |
| S3 | ✔ | [🔨](https://github.com/constellation-rs/amadeus) |
| HDFS | [👐](https://github.com/constellation-rs/amadeus) | [👐](https://github.com/constellation-rs/amadeus) |

✔ = Working<br/>
🔨 = Work in Progress<br/>
👐 = Requested: check out the issue for how to help!
