# Red Hat Scholar
Steps to deploy a Red Hat Scholar page:

1) Fork [https://github.com/redhat-scholars/courseware-template](https://github.com/redhat-scholars/courseware-template) repo and unclick: ‘Copy the master Branch only’. This is because this repo uses a branch named gh-pages to deploy Git Hub pages trough Actions.

![Untitled (1)](https://user-images.githubusercontent.com/95486210/226349082-30cb26d1-4d2e-4392-9040-820197aad154.png)

2) Click ‘Use this template’ then ‘Create new repository’.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dfbad35b-50c4-4b9e-bd8d-9d39f9aea89e/Untitled.png)

3) Click ‘Include all branches’, make it public, give it a name and hit create.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/76f6a39c-5360-48bc-8fe6-0417b4eccd4a/Untitled.png)

4) Once the new repo is created go to ‘Settings’ → ‘Pages’ and verify you have the build and deployment configuration.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f20d8c40-3bc6-4143-b897-bad371830b1c/Untitled.png)

5) In ‘Settings’ → ‘Actions’ → ‘General’ → ‘Workflow permissions’ click ‘Read and write permissions’ and hit ‘Save’, this allow GitHub Actions to redeploy correctly the page when a change in the code is done.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e11ffea5-a3e6-47a1-87e8-cd70debeb909/Untitled.png)

6) Modify ‘site.yml’, it is necessary to change site.url and site.start_page

```jsx
runtime:
  cache_dir: ./.cache/antora

site:
  title: Manual for GitOps workshop
  ##Change url from repo
  url: https://github.com/jtovarro/gitops-workshop-manual
  ##The start_page should be the name of your repo
  start_page: gitops-workshop-manual::index.adoc

content:
  sources:
    - url: ./
      start_path: documentation

asciidoc:
  attributes:
    release-version: master
    page-pagination: true
  extensions:
    - ./lib/tab-block.js
    - ./lib/remote-include-processor.js

ui:
  bundle:
    url: https://github.com/redhat-developer-demos/rhd-tutorial-ui/releases/download/v0.1.9/ui-bundle.zip
    snapshot: true
  supplemental_files:
    - path: ./supplemental-ui
    - path: .nojekyll
    - path: ui.yml
      contents: "static_files: [ .nojekyll ]"

output:
  dir: ./gh-pages
```

7) In ‘Actions’ it is possible to see all the workflows that deployed GitHub pages, and in the ‘Environments’ section you can find the url to the GitHub page deployed.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9ce88e9f-6d45-4e6f-baae-749f804326cd/Untitled.png)

![Untitled](https://user-images.githubusercontent.com/95486210/226348602-4c078e47-0933-4244-bbf7-d87b5d6b2eba.png)


8) To add/remove pages go to ‘documentation/modules/ROOT/pages’ and ‘documentation/modules/ROOT/nav.adoc’ to edit the sections. 

Reference: [https://redhat-scholars.github.io/build-course/rhs-build-course/overview.html#file-structure](https://redhat-scholars.github.io/build-course/rhs-build-course/overview.html#file-structure)

Guide repos: 

[https://github.com/rhte2023-argo-rollouts/redhat-workshop-deployment-strategies](https://github.com/rhte2023-argo-rollouts/redhat-workshop-deployment-strategies)

[https://github.com/acidonper/redhat-workshop-cicd-gitops](https://github.com/acidonper/redhat-workshop-cicd-gitops)
