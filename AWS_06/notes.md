# Amazon Athena
Collect JSON data and API data.

Can be queried using SQL

5 USD per TB

# Amazon QuickSight

An overall dashboard for your data and analytics

# Amazon CloudFront

Content Delivery Network

Temporarily cache website data in edge point locations nearer to users to increase access speed. For production not development. Usually only useful for large companies.

Caches the origin at first access using TTL and at a frequent interval, and then only accesses through the cache.

Cost relative to access amount

Force refresh has to be done through clearing the cache in the server.

DDOS protection, but can also accidentally block genuine uses e.g. multiple company staff trying to access.

## Levels

### S3 Bucket
* Is already part of AWS CloudFront
* Accessed by HTTP (not HTTPS)

### Custom Origin
