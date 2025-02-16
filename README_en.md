# Vault-to-Lockbox Migrator

This script is designed to migrate secrets from [HashiCorp Vault](https://www.hashicorp.com/products/vault) to [Yandex Cloud Lockbox](https://yandex.cloud/services/lockbox).

You can read more about Lockbox in [this article](https://yandex.cloud/blog/posts/2023/04/lockbox-ga).

### What this script can do

 - Verify that connection to Vault is successful by displaying the list of secrets stored there in the console.
 - Export your secrets from Vault to a JSON file. You can edit the file in any editor, e.g., if you do not want to import all Vault contents.
 - Import your secrets from a JSON file to Lockbox. 
 - Delete all secrets from Lockbox using a console command.

### Getting started

1. Install Python 3.8 or higher.
1. For the script to run, its host folder must contain these files:
   * `vault_to_lockbox_migrator.py`: Migration script file.
   * `requirements.txt`: Modules required for the script to run correctly.
   * `.env`: Script configuration parameters.

1. Install the modules (dependencies) by running this command in the console:

   `pip install -r requirements.txt`

1. Fill the `.env` file with the parameters from the below table. 
1. Run the script in the console using this command:

   `python vault_to_lockbox_migrator.py`

1. To import secrets from Vault and transfer them to Lockbox, use the parameters from the below table.

### Constraints

The secrets must be stored with KV version 2 Secrets Engine.

### Script configuration parameters

_Rather than using the `.env` file, you can provide these script parameters in environment variables._

| Parameter         | Default value | Description                                                         | Sample value                        |
|------------------|:----------------------|:-----------------------------------------------------------------|----------------------------------------|
| VAULT_TOKEN      |                       | Token with access permissions to the values of secrets kept in your Vault             | "00000000-0000-0000-0000-000000000000" |
| VAULT_URL        |                       | Vault server address                                              | "https://localhost:8201"               |
| VAULT_ROOT_PATH  |                       | Root path to your secrets vault in Vault                              | "secret"                               |
| VAULT_KV_VERSION | 2                     | KV version of your vault                                              | 2                                      |
| VAULT_VERIFY_SSL | False                 | Disable the certificate verification on Vault API request             | False                                  |
| YC_TOKEN         |                       | Yandex Cloud token with permissions to create secrets in Lockbox | "t1.9euxxx"                            |
| YANDEX_FOLDER_ID |                       | Name of the Yandex Cloud folder to create your secrets in          | "f9sdf9e"                              |
| OUT_FILE         | "secrets.json"        | Name of the file to export Vault secrets into                         | "secrets.json"                          |
| INPUT_FILE       | "secrets.json"        | Name of the file to import Lockbox secrets from                        | "secrets.json"                                     |

### Available command line parameters

| Parameter                       | Description                                                                                                                      |
|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| `-h` or `--help`                  | Help                                                                                                                 |
| `-l` or `--list`                  | Display Vault secrets                                                                                                 |
| `-o` or `--outFile` [filename]    | Output Vault secrets into a file (if no file name is specified, the value of the `OUT_FILE` environment variable will be taken as the file name)            |
| `-m` or `--migrate`               | Migrate all secrets from Vault to Lockbox                                                                                      |
| `-c` or `--createFrom` [filename] | Create Lockbox secrets from a file (if no file name is specified, the value of the `INPUT_FILE` environment variable will be taken as the file name) |
| `-d` or `--deleteAll`             | Delete all secrets from Lockbox                                                                                              |
