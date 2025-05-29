# GH_Certification_Volvo
hello
deploy


#skip workflow o  hotfix branches

jobs:
 test:
  if: "!startsWith(github.ref,'refs/heads/hotfix/')
  runs-on:
  steps:
   run: echo 'run test except for hotfix branch'

   on:
    workflow_dispatch:
    inputs:
     environment:
      required: true
      type: string

  jobs:
   deploy:
    if: startsWith(inputs.environment,'prod')
    runs-on:
    steps:
    run echo ' deploy to prod like env'



    on:
     push:
      paths:
       - '**yml'
       - '**.yaml'
       - '**.json'
  jobs:
   val:
    if: endsWith(github.event.head_commit.message, '.yml')
    steps:
     run: echo ' yaml config modfied  run validation'


  jobs:
   build:
    runs-on:
    steps:
     -name: format the branch name
      run: echo '${{format('Running job on branch {0}' ,github.ref_name)}}' 

     
