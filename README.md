# Data Reporting Python SDK

- Collect your data via ACTE Technology secured gateway


## Installation

- install Python3
- pip3 install git+https://github.com/acte-technology/data-reporting-python-sdk


# Configuration

- Contact ACTE support in order to receive username, password and authorized databases
- copy below code and edit configuration variables

## Example

```python

from acte_data_report_sdk import acte_data_report_sdk
from pprint import pprint
from datetime import datetime, timedelta

# Configuration variables
API_USERNAME = "YOUR_USERNAME"
API_PASSWORD = "YOUR_PASSWORD"
BASE_URL = "https://XXX.acte.ltd"
db = "DATA_DB" # database


# init api class and connect
api = acte_data_report_sdk.ReportApi(BASE_URL)
api.connect(API_USERNAME, API_PASSWORD)

# get allowed databases
databases = api.getDatabases()
pprint(databases)

# get devices
devices = api.getDevices(db)
pprint(devices)
device = "my_device"

# get keys from device
keys = api.getKeys(db, device)
pprint(keys)


# get telemetry data
#    prepare configuration parameters
to_ts = datetime.now().replace(hour=0, minute=0, second=0, microsecond=0).timestamp()
from_ts = ( datetime.now() - timedelta(days=7) ).replace(hour=0, minute=0, second=0, microsecond=0).timestamp()
key = "my_key"
agg_type = "SUM" # aggregation method: AVG | MIN | MAX | SUM
agg_interval = 3600 # aggregation interval in seconds

data = api.getTelemetry(db, device, key, from_ts, to_ts, agg_interval=agg_interval, agg_type=agg_type)
pprint(data)
```
