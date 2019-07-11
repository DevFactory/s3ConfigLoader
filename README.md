# s3ConfigLoader
This python package implements a simple config property loader that can read yaml property files from local or from 
Amazon AWS S3

## Getting Started

**Install:**
```
pip install s3configloader
```


**Usage:**
```python
from s3config.config import Config

config = Config(secrets_path="secrets.yml",
                test_secrets_path="test_secrets.yml",
                secrets_url_var_name="SECRETS_URL")

db_url = config.get_value('DB_URL')
```

sample secrets.yml:
```yaml
app_secrets:
  LDAP_ENABLED: false
  DB_URL: 'localhost:3306'
  DB_PASSWORD: "password"

```

All values in the `app_secrets` are loaded into `Config()`

**Working:**

Config() looks for the property file in this order: 
1. `test_secrets_path` - if `"test"` is passed as a command line arg to your app.
2. `secrets_path`
3. `secrets_url_var_name` - environment variable containing secrets file url (url must be of type `file://` or `s3://`)
