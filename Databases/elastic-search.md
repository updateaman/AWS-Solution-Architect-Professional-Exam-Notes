# ElasticSearch

- May be called Amazon ES in the exam
- Managed version of ElasticSearch (open source project)
- Needs to run on servers (not a serverless offering)
- Use cases:
  - Log Analytics
  - RealTime application monitoring
  - Security Analytics
  - FullText Search
  - Clickstream Analytics
  - Indexing

# ElasticSearch + Kibana + Logstash

- ElasticSearch: provide search and indexing capability
  - You must specify instance types, multi-AZ, etc
- Kibana:
  - Provide real-time dashboards on top of the data that sits in ES
  - Alternative to CloudWatch dashboards (more advanced capabilities)
- Logstash:
  - Log ingestion mechanism, use the "Logstash Agent"
  - Alternative to CloudWatch Logs (you decide on retention and granularity)
