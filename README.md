# Z1A00_WebIDE_template
WebIDE for HANA project template

To adapt the template to your needs and have a first successful build, please do the following:

- global search&replace of 'Z1A00_WebIDE_template' to your HDI container name
  -> this will affect mta.yaml, .pipeline/config.yml and some .txt template files

- project settings:
  set space 'DEV',
  add Git repository parameters 'branch.develop.mergeoptions' = '--no-ff' and 'branch.master.mergeoptions' = '--no-ff'
  
At this point the builds of db folder and the full container should be successful.

There are some .txt files that you can use as templates by removing '.txt' ending and modifying accordingly:
  
- RO_Z1A00_consumer_name_access_grantable.hdbrole.txt:
  rename the file name by replacing 'consumer_name' with the container name which would consume your container and fill the file based on your needs
  
- plain.hdbgrants.txt:
  replace CONTAINER_NAME with the container you want to consume, and which containes the role dedicated to your container
  
- plain.hdbsynonym.txt:
  examples for adding synonyms

- plain.hdbsynonymconfig.txt:
  examples for synonym configuration
  
- mta.yaml.txt:
  (don't remove the .txt because the file is already there)
  the last bullet points in "requires" and "resources" sections are examples which you can add in your existing mta.yaml file, replace CONTAINER_NAME with the respective container
  
Jenkins file is now centralized you can delete that file from your project repo.
