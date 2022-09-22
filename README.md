# Intro To Config Files

This example Cycle project includes some example use cases of utilizing .conf files in your features.

## secrets

This is a simple example where credentials are handled in a .conf file rather than being hard-coded in a .feature or .csv file.  In the default.conf file,
there are just the following entries:
username = ${GROCER_USER}
password = ${GROCER_PASS}
These can be set by having a GROCER_USER and GROCER_PASS environment variable set when Cycle is run. Or utilizing a local.conf file will allow you to 
provide values locally which aren't committed to any code repository. The feature in the secrets folder demonstrates how this works.

## parameterizedTest

This is an example where a default value is included for a parameter (the url used in the test, in this example), and it also allows for that value to be
overridden at run time via an environment variable. This would allow a team to parameterize their tests and inject different values at run time, such as
when executing a test in a CI/CD pipeline. You may want to inject a QA vs Dev environment values or maybe a different warehouse ID, for example.
grocer_url = "https://cyclelabs.io/playground"
grocer_url = ${?GROCER_URL}
This example also moves locators out of the feature and into a config file.  This may be useful where the steps are the same, but locators may change
from one version of an application to the next.

## layeringConfigData

This is an example of having being able to inject different configuration values for different environments while keeping the feature short and without
having to update the feature to run with different configurations. In this example, we are entering an order in the grocer.io application. In the
default.conf file, we have the test data, which includes the price in USD. We also have ca.conf, euro.conf, and yuan.conf which include the test data
from default.conf and overrides the price in a variety of other currencies. In the env.conf, we define the default amongst these to use in the test.
This can be overridden in a local.conf or by setting an ENV_FILE environment variable, so we can easily run the test using a variety of currencies without
having to make any changes to the example.

## combined

In this example, we show a more complete example which combines a variety of the use cases from the previous example. We cleanly separate credential data
from test data (the order entry data in a variety of currencies) from application data (the locators for the web application). In this example we try
to provide an example of how to create a simple, readable, dynamic feature with easy to maintain data.

## sharedConfigData

The previous examples were all intended to be stand alone examples. Thus some config data, like the entries for login credentials,
have been duplicated across each of the folders. But this only for the sake of having isolated examples, and is not required when
using config files.  In this example, I'll show what it would look like when resusable config entries are abstracted out into a
root folder and shared amongst multiple sub folders.
