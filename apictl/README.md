CLI for Importing and Exporting APIs and Applications
=====================================================

For WSO2 API Manager 3.1.0 {#for-wso2-api-manager-3-1.0}
--------------------------

Command Line tool for importing and exporting APIs and Applications
between different API Environments

Getting Started
---------------

-   ### Running

    Select a generated archive suitable for your platform (Mac, Windows,
    Linux) and extract it to a desired location and `cd` into it.\
     Then execute `apictl` to start the application.

    > NOTE: Execute `./apictl` if the working directory is the same
    > where the executable resides
    >
    > Add the location of extracted folder to your system's \$PATH
    > variable to access the executable from anywhere

    Execute `apictl --help` for further instructions.

-   ### Adding Environments

    Add environments by either manually editing
    `$HOME/.wso2apictl/main_config.yaml` or using the command\
     `apictl add-env`.

    > NOTE: Directory structure for configuration files
    > (`$HOME/.wso2apictl`) will be created upon execution of `apictl`

    Execute `apictl add-env --help` for detailed instructions

    > The flags `--environment (-e)` and `--token` are mandatory. You
    > can either provide only the 2 flags `--apim` and `--token`, or all
    > the other 5 flags (`--registration`, `--publisher`, `--devportal`,
    > `--admin`, `--token`) without providing `--apim` flag. If you are
    > omitting any of --registration --publisher --devportal --admin
    > flags, you need to specify --apim flag with the API Manager
    > endpoint.

-   ### Command Autocompletion (For Bash Only) {#command-autocompletion-for-bash-only-}

    Copy the file `apictl_bash_completion.sh` to
    `/etc/bash_completion.d/` and source it with\
     `source /etc/bash_completion.d/apictl_bash_completion.sh` to enable
    bash auto-completion.

* * * * *

Usage
-----

         apictl [command]

#### Global Flags

          --verbose
               Enable verbose logs (Provides more information on execution)
          --insecure, -k
              Allow connections to SSL sites without certs
          --help, -h
              Display information and example usage of a command

### Commands

-   #### login [environment] {#login}

           Flags:
               Optional:
                   --username, -u
                   --password, -p
                   NOTE: user will be prompted to enter credentials if they are not provided with these flags
           Examples:
               apictl login dev -u admin -p admin
               apictl login dev -u admin
               apictl login dev
               cat ~/.mypassword | apictl login dev -u admin

-   #### logout [environment] {#logout}

           Examples:
               apictl logout dev

-   #### export-api

           Flags:
               Required:
                   --name, -n
                   --version, -v
                   --provider, -r
                   --environment, -e
               Optional:
                   --username, -u
                   --password, -p
                   NOTE: user will be prompted to enter credentials if they are not provided with these flags
           Examples:
               apictl export-api -n TestAPI -v 1.0.1 -r admin -e staging
               apictl export-api -n TestAPI -v 1.0.1 -r admin -e staging -u admin -p 123456
               apictl export-api -n TestAPI -v 1.0.1 -r admin -e staging -u admin
               apictl export-api -n TestAPI -v 1.0.1 -r admin -e staging -p 123456

-   #### import-api

<!-- -->

            Flags:
                Required:
                    --file, -f
                    --environment, -e
                Optional:
                    --username, -u 
                    --password, -p 
                    NOTE: user will be prompted to enter credentials if they are not provided with these flags
            Examples:
                apictl import-api -f dev/TestAPI_1.0.0.zip -e dev
                apictl import-api -f qa/TestAPI_2.0.0.zip -e dev -u admin -p 123456
                apictl import-api -f staging/TestAPI_1.1.zip -e dev -u admin
                apictl import-api -f production/TestAPI_3.0.1.zip -e dev -p 123456
                apictl import-api -f TestAPI -e dev

-   #### export-app

           Flags:
               Required:
                    --name, -n
                    --owner, -o
                    --environment, -e
               Optional:
                    --username, -u
                    --password, -p
                    NOTE: user will be prompted to enter credentials if they are not provided with these flags
           Examples:
                    apictl export-app -n SampleApp -o admin -e dev
                    apictl export-app -n SampleApp -o admin -e prod

-   #### import-app

<!-- -->

            Flags:
                Required
                      --file, -f
                      --environment, -e
                Optional
                      --skipSubscriptions, -s
                      --owner, -o
                      --preserveOwner, -r
                      --file, -f
                      --environment, -e
            Examples:
                apictl import-app -f qa/apps/sampleApp.zip -e dev
                apictl Import App -f staging/apps/sampleApp.zip -e prod -o testUser -u admin -p admin
                apictl import-app -f qa/apps/sampleApp.zip --preserveOwner --skipSubscriptions -e staging

-   #### list apis

              Flags:
                  Required:
                      --environment, -e
                  Optional:
                      --username, -u 
                      --password, -p 
                      NOTE: user will be prompted to enter credentials if they are not provided with these flags
                      --query, -q
              Examples:
                  apictl list apis -e dev
                  apictl list apis -e prod -q version:1.0.0
                  apictl list apis -e prod -q provider:admin
                  apictl list apis -e staging

-   #### list apps

              Flags:
                  Required
                          --environment, -e
                          --owner, -o
                    Optional
                          --username, -u
                          --password, -p
                Examples:
                    apictl list apps -e dev -o admin
                    apictl list apps -e staging -o sampleUser

-   #### list envs

             Flags:
                 None
             Example:
                 apictl list envs

-   #### add-env

              Flags:
                Required:
                    --environment, -e (Name of the environment)
                    --token (Token Endpoint)
                    AND
                    --apim (API Manager endpoint)
                    OR (the following 4)
                    --registration https://localhost:9443 \
                    --publisher https://localhost:9443 \
                    --devportal https://localhost:9443 \
                    --admin https://localhost:9443
                Optional:
                    --list (API List endpoint for environment)

                Examples:
                apictl add-env -e dev \
                    --apim https://localhost:9443 \
                    --token https://localhost:8243/token

                apictl add-env -e staging \
                    --registration https://idp.com:9443 \
                    --publisher https://apim.com:9443 \
                    --devportal https://apps.com:9443 \
                    --admin https://apim.com:9443 \
                    --token https://gw.com:8243/token
                    
                apictl add-env -e prod \
                    --apim https://apim.com:9443 \
                    --registration https://idp.com:9443 \
                    --token https://gw.com:8243/token

-   #### remove-env

<!-- -->

            Flags:
                Required:
                    --environment, -e (Name of the environment)
                Examples:
                    apictl remove-env -e dev

-   #### reset-user

<!-- -->

            Flags
                --environment, -e
            Examples:
                apictl reset-user -e dev

-   #### version

              apictl version

-   #### set

              Flags
                  --http-request-timeout
                  --export-directory
              Examples:
                  apictl set --http-request-timeout 10000
                  apictl set --export-directory /home/user/exported

-   #### get-keys

           Flags:
               Required:
                    --name, -n
                    --version, -v
                    --environment, -e
               Optional:
                    --username, -u
                    --password, -p
                    NOTE: user will be prompted to enter credentials if they are not provided with these flags
           Examples:
                    apictl get-keys -n PizzaShackAPI --version 1.0.0 -e dev --provider admin

-   #### delete api

           Flags:
               Required:
                   --name, -n
                   --version, -v
                   --environment, -e
               Optional:
                   --provider, -r
                   NOTE: User will be prompted to enter credentials if the user is not logged in to the environment.
           Examples:
               apictl delete api -n TestAPI -v 1.0.0 -r admin -e staging
               apictl delete api -n TestAPI -v 1.0.0 -e production

-   #### delete api-product

           Flags:
               Required:
                   --name, -n
                   --environment, -e
               Optional:
                   --provider, -r
                   --version, -v
                   NOTE: User will be prompted to enter credentials if the user is not logged in to the environment.
           Examples:
               apictl delete api-product -n TwitterAPI -r admin -e dev
               apictl delete api-product -n FacebookAPI -v 1.0.0 -e production

-   #### delete app

           Flags:
               Required:
                   --name, -n
                   --environment, -e
               Optional:
                   --owner, -o
                   NOTE: User will be prompted to enter credentials if the user is not logged in to the environment.
           Examples:
               apictl delete app -n TestAPI -o admin -e staging
               apictl delete app -n TestAPI -e production

-   #### change-status api

           Flags:
               Required:
                   --action, -a
                   --name, -n
                   --version, -v
                   --environment, -e
               Optional:
                   --provider, -r
                   NOTE: User will be prompted to enter credentials if the user is not logged in to the environment.
           Examples:
               apictl change-status api -a Publish -n TestAPI -v 1.0.0 -r admin -e staging
               apictl change-status api -a Publish -n TestAPI -v 1.0.0 -e production


