# Issue Reporting

Please report your issues here https://github.com/xgenecloud/xgenecloud/issues


# Semantic Release 


1. Configure semantic release
    - Install `@semantic-release/gitlab` and `semantic-release` using following command
        
        ```
        npm install -D @semantic-release/gitlab semantic-release
        ```
    
    - Add following things to `package.json` for adding commit analyzer and github plugins, where specify release files within github options.
        
        ```
         "release": {
            "plugins": [
              [
                "@semantic-release/commit-analyzer",
                {
                  "parserOpts": {
                    "noteKeywords": [
                      "BREAKING CHANGE",
                      "BREAKING CHANGES",
                      "BREAKING"
                    ]
                  }
                }
              ],
              "@semantic-release/release-notes-generator",
              [
                "@semantic-release/github",
                {
                  "assets": [
                    {
                      "path": "release/xgene-0.0.1.dmg",
                      "label": "xgene-0.0.1.dmg"
                    }
                  ]
                }
              ]
            ]
          }
        ```
         Ref : https://github.com/semantic-release/github#usage and https://github.com/semantic-release/github#usage         
         
2. Getting access token from Github
      - Follow following documentation https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line

3. Commit format

    
    | Commit message                                                                                                                                                                                   | Release type               |
    |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
    | `fix(pencil): stop graphite breaking when too much pressure applied`                                                                                                                             | Patch Release              |
    | `feat(pencil): add 'graphiteWidth' option`                                                                                                                                                       | ~~Minor~~ Feature Release  |
    | `perf(pencil): remove graphiteWidth option`<br><br>`BREAKING CHANGE: The graphiteWidth option has been removed.`<br>`The default graphite width of 10mm is always used for performance reasons.` | ~~Major~~ Breaking Release |
        
    
4. Deploying release

    - Set environment variable `GH_TOKEN` with the token generated in step *2*
    - Run following command for publishing release.
        
        ```
       ./node_modules/.bin/semantic-release  --no-ci    
        ```
