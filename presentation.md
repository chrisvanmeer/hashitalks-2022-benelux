%title: How to deploy your HashiCorp stack with Ansible under 15 minutes
%author: Chris van Meer
%date: 2022-12-01

-> # HashiTalks 2022 Benelux <-

How to deploy your HashiCorp stack with Ansible under 15 minutes

*_Agenda_*

* Introduction
    * whoami
    * Why
    * How

* Setup
    * Overview
    * General deployment
    * PKI
    * Consul
    * Vault
    * Nomad
    * Demo app
        * Traefik
        * Web app

* Contact

-------------------------------------------------

-> *_Introduction_* <-

chris@atcomputing ~ $ *whoami*

*Chris van Meer*
Open Source Consultant at AT Computing

*Strong focus on*
Networking, Ansible, HashiCorp portfolio

*Certificates*
* HashiCorp Certified: Consul Associate
* HashiCorp Certified: Terraform Associate
* HashiCorp Certified: Vault Associate
* HashiCorp Certified: Vault Operations Professional
* HashiCorp Consul: Certified HashiCorp Implementation Partner (CHIP)
* HashiCorp Terraform: Certified HashiCorp Implementation Partner (CHIP)
* HashiCorp Vault: Certified HashiCorp Implementation Partner (CHIP)

-------------------------------------------------

-> *_Why_* <-

* Most demos use dev mode
* TLS is always disabled
* Complete integration guide was missing
* Useable as quick test or demo environment
* Most demos use Terraform as default
* Needed something modular

-------------------------------------------------

-> *_How_* <-

```
                               .,,,,,,.                          
                       ,(@@@@@@@@@@@@@@@@@@@@@(                  
                   ,@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@&              
                .@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@           
              %@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@,        
            (@@@@@@@@@@@@@@@@@@@@&   .@@@@@@@@@@@@@@@@@@@@       
           @@@@@@@@@@@@@@@@@@@@@%     .@@@@@@@@@@@@@@@@@@@@#     
          @@@@@@@@@@@@@@@@@@@@@#   (   .@@@@@@@@@@@@@@@@@@@@#    
         @@@@@@@@@@@@@@@@@@@@@#   (@@   .@@@@@@@@@@@@@@@@@@@@(   
        *@@@@@@@@@@@@@@@@@@@@#   #@@@@    @@@@@@@@@@@@@@@@@@@@   
        %@@@@@@@@@@@@@@@@@@@#   #@@@@@@.   @@@@@@@@@@@@@@@@@@@*  
        &@@@@@@@@@@@@@@@@@@(      .@@@@@.   @@@@@@@@@@@@@@@@@@/  
        %@@@@@@@@@@@@@@@@@/   (@(    .@@@.   @@@@@@@@@@@@@@@@@*  
        ,@@@@@@@@@@@@@@@@*   /@@@@@#     &.   @@@@@@@@@@@@@@@@   
         (@@@@@@@@@@@@@@,   /@@@@@@@@@%        @@@@@@@@@@@@@@.   
          &@@@@@@@@@@@@,   /@@@@@@@@@@@@@&      @@@@@@@@@@@@/    
           (@@@@@@@@@@*   (@@@@@@@@@@@@@@@@@@. .@@@@@@@@@@@      
             @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@/       
               @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@%         
                 *@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@.           
                    ,@@@@@@@@@@@@@@@@@@@@@@@@@@@@%               
                         *#@@@@@@@@@@@@@@@@@(.                   
```

-------------------------------------------------

-> *_Setup_ - Overview* <-

```
       +---server1---+     +---server2---+     +---server3---+         
       |             |     |             |     |             |         
       | Consul (C)  |     | Consul (C)  |     | Consul (C)  |         
       | Vault  (V)  | <-> | Vault  (V)  | <-> | Vault  (V)  |         
       | Nomad  (N)  |     | Nomad  (N)  |     | Nomad  (N)  |         
       |             |     |             |     |             |         
       +-------------+     +-------------+     +-------------+         
              +-------------------+-------------------+
                                  |
                                  +                    
+---client1---+   +---client2---+   +---client3---+   +---client4---+
|             |   |             |   |             |   |             |
|  C + V + N  |   |  C + V + N  |   |  C + V + N  |   |  C + V + N  |
|  ---------  |   |  ---------  |   |  ---------  |   |  ---------  |
|   Traefik   |   |   Web App   |   |   Web App   |   |   Web App   |
|             |   |             |   |             |   |             |
+-------------+   +-------------+   +-------------+   +-------------+
```


-------------------------------------------------

-> *_Setup_ - General Deployment* <-

* Multipass / Terraform
    * Deploys instances
    * Creates Ansible inventory
    * Modifies local hosts file

Playbook run took 0 days, 0 hours, 2 minutes, 38 seconds

* Pre-requisites
    * apt packages
    * hashicorp repository

Playbook run took 0 days, 0 hours, 5 minutes, 7 seconds

-------------------------------------------------

-> *_Setup_ - PKI* <-

-------------------------------------------------

-> *_Setup_ - Consul* <-

-------------------------------------------------

-> *_Setup_ - Vault* <-

-------------------------------------------------

-> *_Setup_ - Nomad* <-

-------------------------------------------------

-> *_Setup_ - Traefik* <-

-------------------------------------------------

-> *_Setup_ - Demo App* <-

-------------------------------------------------

-> *_Resources_* <-

-> [Presentation](https://github.com/chrisvanmeer/hashitalks-2022-benelux)
-> [GitHub Repository](https://github.com/chrisvanmeer/at-hashi-demo) <-

-------------------------------------------------

-> *_Contact_* <-

Email          [c.v.meer@atcomputing.nl](mailto:c.v.meer@atcomputing.nl)
Website        [chrisvanmeer.nl](https://chrisvanmeer.nl)
GitHub         [@chrisvanmeer](https://github.com/chrisvanmeer)
LinkedIn       [chrisvanmeer](https://linkedin.com/in/chrisvanmeer)
Reddit         [u/chrisvanmeer](https://www.reddit.com/user/chrisvanmeer)
               [r/hashicorp](https://www.reddit.com/r/hashicorp)
               [r/consul](https://www.reddit.com/r/consul)
Discord        [The DevOps Lounge](https://discord.gg/devopslounge)
Meetup         [Amsterdam HashiCorp User Group](https://www.meetup.com/amsterdam-hashicorp-user-group)
