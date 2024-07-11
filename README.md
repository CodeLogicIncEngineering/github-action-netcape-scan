## About

GitHub Action to scan .Net artifacts into a CodeLogic server using the CodeLogic .Net Agent.


### Example

```yaml
name: codelogic-scan

on:
  push:
    branches: [ "integration" ]
  pull_request:
    branches: [ "integration" ]
  workflow_dispatch:
    
jobs:
  codelogic-scan:
    name: Perform CodeLogic Scan
    environment: CodeLogic Scan Env
    runs-on: ubuntu-latest
    steps:
      - name: Check out the repo
        uses: actions/checkout@v4
      - name: Run the CodeLogic Scan
        uses: CodeLogicIncEngineering/codelogic-java-agent-github-action@integration
        with:
          version: latest
          codelogic_host: ${{ vars.CODELOGIC_HOST }}
          agent_uuid: ${{ secrets.AGENT_UUID }}
          agent_password: ${{ secrets.AGENT_PASSWORD }}
          application_name: MyApplication
          scan_space: default
          scan_depth: 1
          recursive_filter: com.example
          method_filter: com.example
```


## Customizing


| Name                    | Type    | Description                                                                                                                                                                                             |
|-------------------------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `version`               | String  | The version of the agent docker image to use. Default is latest.                                                                                                                                        |
| `codelogic_host`        | String  | The host address of the CodeLogic instance without the "/codelogic/ui/" part.                                                                                                                           |
| `agent_uuid`            | String  | The UUID of the Agent in CodeLogic.                                                                                                                                                                     |
| `agent_password`        | String  | The password for the agent.                                                                                                                                                                             |
| `application_name`      | String  | The Application node to create that will be the parent of all objects found in the scan.                                                                                                                | 
| `scan_space`            | String  | The name of the scan space that the data will be saved to. If specified, a ScanSpace with this name will be created if not found. If not specified, information will be saved to the default ScanSpace. | 
| `scan_path`             | String  | A comma-separated list of files and folders to scan. Must start with /github/workspace/. Defaults to /github/workspace                                                                                  |
| `scan_path_depth`       | String  | During scanning, this value will be used as the depth of subdirectories to traverse before stopping. Defaults to 1.                                                                                     |
| `recursive_filter`      | String  | A comma-separated list of substrings to key off of to trigger recursive analysis (jar within jar).                                                                                                      |
| `method_filter`         | String  | A comma-separated list of Java package prefixes that should be included in method-invokes-method relationships.                                                                                         |
| `database_identities`   | String  | A comma-separated list of database identities to use in the creation of relationships.                                                                                                                  |
| `force_rescan`          | boolean | Forces jCape to rescan already scanned artifacts. Defaults to false.                                                                                                                                    |
| `expunge_scan_sessions` | boolean | Instruct the server to delete all other scan sessions created by this agent and its configuration after the current scan session has completed successfully. Defaults to false.                         |
| `java_opts`             | String  | Java options to pass to the java command.                                                                                                                                                               |

