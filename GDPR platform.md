# GDPR notes

### Masking
There are several masking techniques that we could use
- K-anonymization
- Encryption 
  - Today we are already quite heavy users of this, using cloud cmek on bigquery
    etc.
- Redaction
- Tokenization

## Architecture
Its a really good idea to separate both logically and physically the storage of
sensitive and non-sensitive data.
