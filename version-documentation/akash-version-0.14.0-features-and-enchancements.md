# Akash Version 0.14.0 Features & Enchancements

## **Prerequisites**

The sections which follow detail Akash deployment configuration and management features introduced in version 0.14.0.  Ensure the Akash CLI version is upgraded to 0.14.0 prior to command execution and usage.

The SDL code samples encompassed throughout this guide are available in the “Full SDL Code Base Utilized” section as a single complete code base.

## **Deployment Shell Access**

Abilities to manage deployed Akash containers have been accentuated greatly within this release.  Introduced deployment capabilities include:

* Ability to execute commands within running Linux containers/Akash deployments.  Such an ability resembles “docker exec” command execution within a live container instance.
* Ability to gain access to the CLI/shell of a running Linux container/Akash deployment.
* Ability to remote copy files from running Linux containers/Akash deployments to a local file instance for inspection.

In the subsections which follow granular details of these introduced features will be explored with example executions and depictions. 

### **Remote Shell Command Execution**

_Execute command sets within a running Akash deployment_

* Command template with variable bracketing as such &lt;variable-name&gt;
* Notes of interest pertaining to command execution:
  * The service-name variable must match the service value in the deployment’s SDL.  For example - in the depicted segment of an SDL file below - the service-name in remote shell execution would be “web”

![](https://lh3.googleusercontent.com/BgF4dAJD-W3HKaLJM4xvmLk-BWxN7-OjD5QknE7kWV9K938u3MTZj0slv5VgFd8eC41QF0JmUtzcc4pCcu5PbG-HhgtDp7QCfIokY5AI1vlewgDo1E4QMKo4AXsUMMQOw7USXjSa=s0)

```text
akash provider lease-shell --from <key-name> --dseq <dseq-number> --provider=<provider-address> <service-name> <command-to-execute>
```

* Example command fully populated

```text
akash provider lease-shell --from mykey --dseq 226186 --provider=akash1gx4aevud37w4d6kfd5szgp87lmkqvumaz57yww web cat /etc/passwd
```

* Example command fully populated using environment variables
* Prior establishment of the AKASH\_KEY\_NAME and AKASH\_PROVIDER environment variables would be necessary to allow this syntax

```text
akash provider lease-shell --from $AKASH_KEY_NAME --dseq 226186 --provider=$AKASH_PROVIDER web cat /etc/passwd
```

* Expected output example

![](https://lh4.googleusercontent.com/ME0D00NtelEkGHbiFQYO66gBbrPGs3IvyeNADitplLF2AE6h4JK-iaNCGEQ2C5qd2636lYvdRJRAXTnfFwGdYcJSKOe5TVtF_sb3jDvbtfaQOFeyod8m3d146FB9Ga6eTJ49Cvu4=s0)

### **Access the Deployment Shell \(CLI\)**

_Gain access to an active Akash deployment’s CLI/shell_

* Command template with variable bracketing as such &lt;variable-name&gt;
* Command notes of interest:
  * The service-name variable must match the service value in the deployment’s SDL.  For example - in the depicted segment of an SDL file below - the service-name in remote shell execution would be “web”
  * Note the “tty” switch dictating desire for shell/CLI access

![](https://lh3.googleusercontent.com/BgF4dAJD-W3HKaLJM4xvmLk-BWxN7-OjD5QknE7kWV9K938u3MTZj0slv5VgFd8eC41QF0JmUtzcc4pCcu5PbG-HhgtDp7QCfIokY5AI1vlewgDo1E4QMKo4AXsUMMQOw7USXjSa=s0)

```text
akash provider lease-shell --from <key-name> --dseq <dseq-number> --tty --provider=<provider-address> <service-name> /bin/sh
```

* Example command fully populated
* Note - the container instance must have a /bin/sh shell for the command to work in this exact syntax.  If this were an Alpine container base image /bin/sh would need to become /bin/ash and this serves as an example of possible edit to the command syntax based on container type.

```text
akash provider lease-shell --from mykey --dseq 226186 --tty --provider=akash1gx4aevud37w4d6kfd5szgp87lmkqvumaz57yww web /bin/sh
```

* Example command fully populated using environment variables
* Prior establishment of the AKASH\_KEY\_NAME and AKASH\_PROVIDER environment variables would be necessary to allow this syntax

```text
akash provider lease-shell --from $AKASH_KEY_NAME --dseq 226186 --tty --provider=$AKASH_PROVIDER web /bin/sh
```

* Expected output example
* Note - Linux commands “pwd” and “ls” are included and as executed within the deployment to validate Akash container shell access

![](https://lh6.googleusercontent.com/6Bd4MCrhU71vIM5OzREMlV8DdxaSEO2T80PNzFJVO91mVrkDYzdBIZ45V10Crcazvpi6afl3ojocnUu_8bnPgxHflJ6WJuZFvZsZpfcf19wna1xs1akzCEnNzghJLJP_xYsVOB2F=s0)

### **Copy File from Akash Container/Deployment**

_Copy a file from an active Akash deployment to a local file instance for inspection_

* Command template with variable bracketing as such &lt;variable-name&gt;
* Command notes of interest:
  * The service-name variable must match the service value in the deployment’s SDL.  For example - in the depicted segment of an SDL file below - the service-name in remote shell execution would be “web”

![](https://lh3.googleusercontent.com/BgF4dAJD-W3HKaLJM4xvmLk-BWxN7-OjD5QknE7kWV9K938u3MTZj0slv5VgFd8eC41QF0JmUtzcc4pCcu5PbG-HhgtDp7QCfIokY5AI1vlewgDo1E4QMKo4AXsUMMQOw7USXjSa=s0)

```text
akash provider lease-shell --from <key-name> --dseq <dseq-number> --provider=<provider-address> <service-name> <command-to-execute> > <local-file-name>
```

* Example command fully populated

```text
akash provider lease-shell --from mykey --dseq 226186 --provider=akash1gx4aevud37w4d6kfd5szgp87lmkqvumaz57yww web cat /etc/passwd > local_copy_of_passwd
```

* Example command fully populated using environment variables
* Prior establishment of the AKASH\_KEY\_NAME and AKASH\_PROVIDER environment variables would be necessary to allow this syntax

```text
akash provider lease-shell --from $AKASH_KEY_NAME --dseq 226186 --provider=$AKASH_PROVIDER web cat /etc/passwd > local_copy_of_passwd
```

* Expected output example
* Note - Linux command “ls” and “cat” are included in the depiction to validate successful file copy from remote Akash container/deployment to local file

![](https://lh4.googleusercontent.com/cJd-e86o-vYhhPNsfLsOjxEXDM7Sb8d-AMkpjj5W8VJ9E0ynO-6RN_nzHQIinb00vPgm8xfj0njYBw5-_CqBuajPqE-sKcxrqkaehfF5Gf9RXiVJf27khnNxbm3lmYWtqTLN2Rfy=s0)

## **Deployment HTTP Options \(SDL Definitions\)**

Akash deployment SDL services stanza definitions have been augmented to include “http\_options” allowing granular specification of HTTP endpoint parameters.  Inclusion of the parameters in this section are optional but will afford detailed definitions of attributes such as body/payload max size where necessary.

### **Overview**

The following “http\_options” have been introduced in this version.  In subsequent sections of this guide the placement of “http\_options” within the SDL services stanza will be detailed.  


* _**Max\_body\_size**_ - sets the maximum size of an individual HTTP request body
* _**Read\_timeout**_ - duration the proxy will wait for a response from the service 
* _**Send\_timeout**_ - duration the proxy will wait for the service to accept a request
* _**Next\_cases**_ - defines the cases where the proxy will try another replica in the service.  Reference the upcoming “Next Cases Attribute Usage” section for details pertaining to allowed values.
* _**Next\_tries**_ - number of attempts the proxy will attempt another replica

### **Example HTTP Options Usage**

* Depiction displays the placement and structure of the http\_options key within the greater services section and within a specific service’s expose key.
* Service section of the greater SDL isolated for focus.

![](https://lh4.googleusercontent.com/oXXBUSlWyFomOTKfA0z38maeEkdc-Y264KAukd0bnLByiQRDB6l3Qwa43jYmfk-Q4N6CXC7p5PPwqSobCOuVBKlaQUko9HTAJU1SJq_Yyv6AOgv2Z3dKOlQxkoHwJ-yyMv0eRy_e=s0)

* Depiction displays the placement of http\_options within the entire, greater SDL definition

![](https://lh3.googleusercontent.com/cOrxEtOvXzyhPHbEpA_DI06km8v627RJZEmGlPFqE41k8N5I53DBGsEi3lXbxYewvjCUiN9fP9qItPC5E0zNOV8jkQYrl2sIREPnafu_k9zleNN1HKSYboFQR40U01o_P22limIC=s0)

### **Next Cases Attribute Usage**

The “http\_options” key of “next\_cases” accepts an array of values which may contain one or more of the following values.  When included in the “next\_cases” array value - the specified HTTP response code/message will provoke an attempt to service the request by one of the other container members/replicas of the deployment.  The “next\_cases” attempt to service via an additional container will only provoke if the SDL defines a count of greater than one \(1\).  A deployment with a count of one \(1\) would have no other replicas to facilitate the additional service attempt. 

* “error”
* “timeout”
* “403”
* “404”
* “429”
* “500”
* “502”
* “503”
* “504”
* “off”

## **Hostname Migration**

Deployment of an updated workload encounters a challenge when the DNS hostname remains active on the existing deployment.  An example scenario is presented to ensure understanding of the challenge - followed by a review of the mechanism introduced in this release to migrate a hostname to the new deployment.

### **Overview of Hostname Migration Need**

In this scenario two identical deployments will be launched mimicking an initial instance/deployment and a secondary updated deployment.

The following SDL is utilized in this example.  Note the presence of the highlighted accept key dictating the DNS name of the deployment \(supermariotest.akash.network\).  
****

![](https://lh6.googleusercontent.com/aXCyB9D5ScqRmD6ZfBQbI56wZkpQdlxj38AKc3wKB-_tmJR2DXbsPNo1S7nQgqByR5ejykf_MgxO57HUghtFqeKLZVYfBtKT-rb8gIcLiVPKQ9updFikKNRm-aSZeQ31vXyT-MXP=s0)

* Two instances of the deployment are provoked \(referred to as “OriginalDeployment” and “UpdatedDeployment” in this guide for clarity\)
* The OriginalDeployment lease status displays URIs for both the Akash full domain name \(ending in akashian.io\) and the SDL specified domain name of “supermariotest.akash.network”
* Note - the DSEQ for this deployment is - 241027.  The DSEQ reference point will be of importance for later validations.

![](https://lh6.googleusercontent.com/xaohN1p97gj1v_kyGOX5-4CtMxf25bZp9GGom9s8JH-KFwZ_zSE6O_o0yBiNavdaeMtUS15bfsuZEJCo0Qe7PBtebU8CPuAVcQXavfWa_N1zMAU2EcpQHDRUUhT-RcFS8jb9QEuT=s0)

* The UpdatedDeployment lease status displays a single URI - the Akash full domain name \(ending in akashian.io\) - and the SDL specified domain name of “supermariotest.akash.network” is not present
* The hostname of “supermariotest.akash.network” was not migrated when the new deployment generated despite the declaration of the hostname in the SDL’s accept key-value pair
* If the initial deployment \(OriginalDeployment\) had been destroyed prior to the creation of the upgraded instance \(UpdatedDeployment\) the hostname would have been free and the new deployment would have assumed this domain name per the SDL specification.
* But often to ensure continuity of services the desirable strategy would be to activate the new instance prior to removing a pre-existing instance and only migrate production traffic to a readied upgraded instance.
* The hostname migration commands introduced - and discussed subsequently - allows such graceful migration.
* Note - the DSEQ for the UpdatedDeployment is - 241064.  The DSEQ reference point will be of importance for later validations.

![](https://lh5.googleusercontent.com/lofd32uDsrfnWKWeUwxtxkgj9B_z0hSwJevZJ5YHusIlXPLm-TXYoFmxiM6XCeWiG0IEOm7OD0qnWBpfN47uTcnIT8bxQGsEJ0VXgETiZLrqXVJ5qOhjst9QOcOVhX6cfVG-DeW9=s0)

### **Hostname Migration Command**

The example hostname migration will continue with the two deployment scenarios provoked in the prior sub-section.

* Hostname migration command syntax with variable bracketing as such &lt;variable-name&gt;

```text
akash provider migrate-hostnames --from <key-name> --dseq <dseq-number> --provider=<provider-address> <hostname>
```

* Example, populated hostname migration command
* In referencing the deployment DSEQ the hostname is migrated to the UpdatedDeployment instance with a DSEQ of 241064 and simultaneously removing the hostname from OriginalDeployment \(DSEQ 241027\)

```text
akash provider migrate-hostnames --from mykey --dseq 241064 --provider=akash1gx4aevud37w4d6kfd5szgp87lmkqvumaz57yww supermariotest.akash.network
```

### **Validation of Hostname Migration**

#### **Hostname/URI Configuration Validations**

Validations of hostname migration are provided in the sample OriginalDeployment and UpdatedDeployment scenario.  


* The lease-status command is utilized in the section to display active URIs/hostnames associated with specific deployments
* The syntax for the lease-status command is as follows

```text
akash provider lease-status --node $AKASH_NODE --home ~/.akash --dseq $AKASH_DSEQ --from $AKASH_KEY_NAME --provider $AKASH_PROVIDER
```

* In the depiction which follows the state of the OriginalDeployment instance proves:
  * Prior to the migrate-hostnames command invoke the hostname specified in the SDL is married to the instance
  * The migrate-hostnames command is invoked specifying the DSEQ of the upgraded deployment instance
  * Post invoke of migrate-hostnames the SDL specified hostname is no longer married to the original instance

![](https://lh3.googleusercontent.com/NjH7BDfxfVsmlG7ct9jmf2yPBJmGGKyt4jwJ4_N9d2Zpqv1Xlr9MaXCjNlI9jGWduoDwieu2324H91qxI7Kuwau8yNGLOFYYyHtnQhXqTol8ApStJkOD3l6ZtUqa07n1o_8IgtoY=s0)

* In the depiction which follows the state of the UpgradedDeployment instance proves:
  * Post migrate-hostnames command invoke the hostname has been migrated to the upgraded deployment instance
  * If desired and in an event in which the upgrade deployment was not servicing traffic correctly - the hostname could be migrated back to OriginalDeployment using the identical migrate-hostname command set but with the OriginalDeployment DSEQ specified

![](https://lh5.googleusercontent.com/hfSpUr7G2msOv-IseXC-thWYLtNNeRU46ZwmwPdMq94duq_DzpVjQlN-tkBOyNvFau788DzsdS2HfDmWTBnjLFKdg8gudVv6aID9YOFjdMA4uyGp0iePaPYV4C0S0z80f_G3Pz0F=s0)

#### **Connectivity Test Validations**

As discussed prior - in a production environment it may be advantageous to leave the pre-existing deployment \(I.e. OriginalDeployment in this guide’s scenario\) in place post migration for possible fallback scenarios.  But to validate connectivity has migrated successfully - the legacy deployment will be removed in our example scenario to prove connectivity to the upgraded deployment post hostname migration.

* Prior to hostname migration a CuRL test was conducted to the pre-existing deployment \(OriginalDeployment\).  At the time of this test the upgraded deployment did not exist.  A CuRL header rewrite is utilized to successfully test connectivity to the hostname \(supermariotest.akash.network\).

```text
curl --header 'Host: supermariotest.akash.network' 2gkpg7qhghetb7tu1ku9aspbl8.wwwp1.h18.akashian.io
```

![](https://lh5.googleusercontent.com/UNii0_mjtEGvVNxuh-u3-h41kAKuCWJWtIMJtM3URMwxfsVcYHN8JhevX7XiZ3HqLnNMrIIviYiAUzbURD2uM71xwiJ6s6pkbZNNd54od_xSps4cTRnRd1eh6We1F7XoWSVFpXRo=s0)

* Post deployment  of the upgraded instance and hostname migration - the pre-existing deployment is removed, connectivity to the hostname via CuRL is conducted anew, and the successful HTML response validates the hostname was migrated properly.

```text
curl -v --header 'Host: supermariotest.akash.network' t3r1sn9c5991beqe90hfu6facg.wwwp1.h18.akashian.io
```

![](https://lh5.googleusercontent.com/WplSAKrIfP_NK6sMP7XoJMKRdwtKyA0Q6g2rhdOl1SgMh02KV0l3w1aE0KGwNH_uhW9_x-9YFJRUwwTynGJ_gJ31L3sDHtkYEoNYNXpwB5u72yko9stYE8n_Es-PzK1wJDlRnkaN=s0)

### **Requirements and Limitations of Migrate Hostname**

#### **DNS CNAME Update**

* When planning a hostname migration ensure that proper public DNS record updates are planned and executed to limit interruption in services.
* In the example scenario utilized and to highlight necessary public DNS record adjustments:
  * The organization owning the akash.network DNS record would have a DNS canonical name \(CNAME\) record for supermariotest.akash.network pointing to the Akash deployment destination of 2gkpg7qhghetb7tu1ku9aspbl8.wwwp1.h18.akashian.io \(OriginalDeployment\)
  * The organization would need to update the CNAME record once the hostname migration was completed to the destination of t3r1sn9c5991beqe90hfu6facg.wwwp1.h18.akashian.io \(UpgradedDeployment\)
  * An interruption in service may be provoked as the public DNS records are published and distributed

#### **Requirements**

* A domain name migration may be migrated to any deployment associated with the same wallet. 
* The hostname must be declared in the SDL’s accept key-value pair of the deployment to allow use of the migrate-hostnames command.

#### **Limitations**

* A domain name used by another wallet may not be utilized.  This is a pre-existing limitation - there may not be conflicts in domain names across wallets - and re-emphasizing to ensure clarity that this limitation remains.

## **SDL Example Utilized**

Full SDL code samples used throughout this guide

```text
---
version: "2.0"
services:
 web:
   image: pengbai/docker-supermario
   expose:
     - port: 8080
       as: 80
       to:
         - global: true
       http_options:
         max_body_size: 3145728
         read_timeout: 50000
         send_timeout: 51000
         next_cases: ["error", "500"]
         next_tries: 2
       accept:
         - supermariotest.akash.network
profiles:
 compute:
   web:
     resources:
       cpu:
         units: 0.1
       memory:
         size: 512Mi
       storage:
         size: 512Mi
 placement:
   westcoast:
     signedBy:
       anyOf:
         - "akash1365yvmc4s7awdyj3n2sav7xfx76adc6dnmlx63"
     pricing:
       web:
         denom: uakt
         amount: 3000
deployment:
 web:
   westcoast:
     profile: web
     count: 1
```

