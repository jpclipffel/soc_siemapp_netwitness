# SOC / SIEM Application / NetWitness (RSA)

A Python 2.6 script which push alerts from RSA to the SOC.


## Components
* `soc_siemapp_netwitness.py`: the Python script which receives, process and forwards RSA alerts;
* `static/template.ftl`: the RSA alerts' template (Freemarker);
* `examples`: various alerts examples


## Script

### Usage
The script is designed to be called by RSA NetWitness. It can be invoked
manually with the list of alerts (as JSON string) as arguments:
```
$> python2.6 soc_siemapp_netwitness.py '{}' '{}' ...
```

You may find alerts example in the file `examples/rsa_script_call_arguments`.

### Configuration
The script have three configuration option written at the top of the file:
* `LOG_FILE`: The script's log file (default: `"/home/notification/soc_siemapp_netwitness.log"`)
* `LOG_HOST`: The {Arc|Eye}Sight connector IP (default: `"10.0.113.13"`)
* `LOG_PORT`: The {Arc|Eye}Sight connector port (default: `514`)

### Behaviour
The script expects JSON alerts as arguments (you may find a full example
in `examples/alert.json`). Each alert passed as argument will be parsed,
validated and send to the specified {Arc|Eye}Sight interface.

If an alert cannot be parsed or validated, **a new one will be generated
and sent** to alert the SOC about thr error.
