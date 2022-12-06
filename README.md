# Heroku Git-Secret Buildpack
Utilises the [git-secret](https://git-secret.io/) library to decrypt secret files within your repository for various purposes such as configuration, 3rd party key/secret storage etc. 

Installs Gawk, Git Secret and uses the `GPG_PRIVATE_KEY` environment variable as the identifier.

## Usage

1. [Create a GPG Key](https://git-secret.io/git-secret#using-gpg) for suitable user e.g: heroku@domain.com
2. Remember to add access for that user to the repository and push up changes:
   ```
    git secret tell heroku@domain.com
    git secret reveal; git secret hide -d
    ```
3. [Follow the steps](https://git-secret.io/git-secret#using-git-secret-for-continuous-integration--continuous-deployment-cicd) to get the private key
```
gpg --armor --export-secret-key heroku@domain.com | tr '\n' ','
```
 
4. Add the key above to an env variable named `GPG_PRIVATE_KEY` on your heroku instance
5. Optionally if you added a password to the gpg key at generation, set a `GPG_PASSPHRASE` env variable
