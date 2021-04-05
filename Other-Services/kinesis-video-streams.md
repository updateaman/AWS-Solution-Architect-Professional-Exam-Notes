# Kinesis Video Streams

- One video stream per streaming device (producers)
  - Security cameras, body worn camera, smartphone
  - Can use a Kinesis Video Streams Producer Library
- Underlying data is stored in S3 (but we don't have access to it)
- Cannot output the stream data to S3 (must build custom solution)
- Consumers:
  - Consumed by EC2 instances for real time analysis, or in batch
  - Can leverage the Kinesis Video Stream Parser Library
  - Integration with AWS Rekognition for facial detection

