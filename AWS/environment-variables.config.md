# environment-variables.config

## Sample 
````yaml
# You must place this file in .ebextensions
# And must have a .config file name
# So the file is at  .ebextensions/environment-variables.config
# Note: Even though the markup language is YAML, you must use use .config extension

option_settings:
  # See: https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/command-options-general.html#command-options-general-elasticbeanstalkapplicationenvironment
  aws:elasticbeanstalk:application:environment:
    DB_URL: "jdbc:postgresql://rds-url-here.com/db"
    DB_USER: username
    
# This format works too:
# option_settings:
#   _ namespace: namespace
#     option_name: option name
#     value: option value

# See: https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/ebextensions-optionsettings.html
````
