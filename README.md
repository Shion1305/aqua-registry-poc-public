## aqua-registry-poc-public

This is a public repository to showcase how to set up a custom aqua registry.

```bash
## This might be required to disable the built-in policy validation feature.
export AQUA_DISABLE_POLICY=true
aqua i
```

## To set up private registry

1. Clone this repository
2. Ensure you have `gh` (GitHub CLI) installed.
3. Run this command and push this repository as a private repository.

    ```shell
    gh repo create --private aqua-registry-poc-private --remote private
    ```

4. Create and push a tag.

    ```bash
    git tag v1 && git push private main --tags
    ```
5. Issue a Personal Access Token and configure your environment.

    1. Open [github.com/settings/tokens/new](https://github.com/settings/tokens/new)
    2. Select `repo` scope
    3. Proceed to `Generate token`. You will get a PAT on the next page.
    4. Set your PAT as environment variable `GITHUB_TOKEN`
    
> [!IMPORTANT]
> I recommend you not execute `export GITHUB_TOKEN=xxx` directly from the terminal, as it persists the key in your command history.
> Use `.envrc.example` to configure your environment safely.
> ```bash
> cp .envrc.example .envrc
> # Fill in your PAT in `.envrc`
> source .envrc
> ```
    
    
6. Modify `aqua.yaml` and point to your private repository.

    ```diff
    diff --git a/aqua.yaml b/aqua.yaml
    index 62f9cdc..cd02339 100644
    --- a/aqua.yaml
    +++ b/aqua.yaml
    @@ -1,9 +1,10 @@
     ---
     registries:
     - type: github_content
    -  name: public
    -  repo_owner: Shion1305
    -  repo_name: aqua-registry-poc-public
    +  name: private
    +  repo_owner: MyUsername
    +  repo_name: aqua-registry-poc-private
    +  private: true
       path: registry.yaml
       private: true
       ref: v1
    ```

7. Ensure you have `aqua.yaml` in your current directory, then run  `aqua i`. It should introduce packages in your environment.
