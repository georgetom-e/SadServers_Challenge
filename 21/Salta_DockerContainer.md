Description: There's a "dockerized" Node.js web application in the /home/admin/app directory. Create a Docker container so you get a web app on port :8888 and can curl to it. For the solution to be valid, there should be only one running Docker container.

Test: curl localhost:8888 returns Hello World! from a running container.



Solution: 

1. Notice the error when you try to run a container from the app image: 

        node:internal/modules/cjs/loader:928
          throw err;
          ^
        
        Error: Cannot find module '/usr/src/app/serve.js'
            at Function.Module._resolveFilename (node:internal/modules/cjs/loader:925:15)
            at Function.Module._load (node:internal/modules/cjs/loader:769:27)
            at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:76:12)
            at node:internal/main/run_main_module:17:47 {
          code: 'MODULE_NOT_FOUND',
          requireStack: []
        }


The Dockerfile that was used to build this app image incorrectly attempts to run a non-existent serve.js file instead of the existing server.js file. 


2. Correct Dockerfile and Build a New Image
     
       vi Dockerfile --> server.js 
       
       sudo docker build -t correct_app . 

3. Run New Image
   
        sudo docker run -d -p 8888:8888 correct_app
