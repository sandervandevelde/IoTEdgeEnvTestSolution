# IoTEdgeEnvTestSolution

Demonstration of reading custom environment variables by an Azure ioT Edge module. 

When the module starts, a number of environment variables are read.

_Note_: This includes the already used Azure IoT Edge module specific variables. Check the example below. 

## Docker container

The current docker container is available at 'svelde/envtestmodule:0.0.1-amd64' (Please check Docker Hub for more recent versions).

## Envrionment variables

The current implementation looks for these variables:

- variableString
- variableJSON

if one of these is not available, it will be marked are missing.

### variableString

Just past any string.

### variableJSON

Pass a JSON formatted text with these two variables:

```
{
    "someInteger" : 42,
    "someString" : "Hello module"
}
```

## Example output

The following output is to be expected:

```
IoT Hub module client initialized.
Start reading environment variables:
GetEnvironmentVariables: 
  IOTEDGE_GATEWAYHOSTNAME = edge-device-test-weu-vm
  IOTEDGE_DEVICEID = MessageTest1-1
  IOTEDGE_WORKLOADURI = unix:///var/run/iotedge/workload.sock
  DOTNET_RUNNING_IN_CONTAINER = true
  IOTEDGE_MODULEGENERATIONID = 637933928617587066
  IOTEDGE_AUTHSCHEME = sasToken
  ASPNETCORE_URLS = http://+:80
  HOME = /home/moduleuser
  PATH = /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
  variableString = HelloVariable
  IOTEDGE_IOTHUBHOSTNAME = xyz.azure-devices.net
  variableJSON = { "someInteger" : 42, "someString" : "Hello module" }
  HOSTNAME = ef033
  IOTEDGE_MODULEID = envtest
  IOTEDGE_APIVERSION = 2019-01-30
  RuntimeLogLevel = Information

Found 'HelloVariable'
Found '{ "someInteger" : 42, "someString" : "Hello module" }', containing '42' and 'Hello module'
End reading environment variables.
```

As you can see, both the Azure IoT Edge module specific variables and our custom environment variables are shown.

## Usage

This is an alternative to sending Desired properties allthough the impact is there.

The environment variable can only be updated using the Deployment manifest. Each time a deployment manifest is sent, all (other) modules will reload their desired properties. 
