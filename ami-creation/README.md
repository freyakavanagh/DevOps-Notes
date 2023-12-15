# AMI: Amazon Machine Image

- A snapshot of your disc, an Exact replica of the data on the disc e.g. maven, JDK, repo
- Means that everything is installed so all you have to do is run the app
- Takes much less time

<u>Steps</u>

1. Instance>Actions>Images and Templates>Create Image
2. Image name and discription
3. Add New Tag: Name, tech242-freya-ready-to-run-java-atlas-app-ami
4. Launch Instance from AMI
5. Fill in details as normal (but already has an image)
6. In User data run the app...
   -  #!/bin/bash
   -  cd repo
   -  sudo mvn spring-boot:start
7. Connect to through the web
