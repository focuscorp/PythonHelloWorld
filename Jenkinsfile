pipeline {
   agent none
   stages {
       stage('Build') {
         agent {
              docker {
                 image 'python:3-alpine'
              }
          }
          steps {
               sh 'echo "hello world"'
               //sh 'python -m py_compile sources/*.py'
               stash(name: 'app-content', includes: '*')
               //stash(name: 'setUpPy', includes: 'setup.py*')
               //stash(name: 'pypirc', includes: '.pypirc')
               //stash(name: 'procfile', includes: 'Procfile')
               //stash(name: 'managePy', includes: 'manage.py')
          }
       }


     stage('Packaging') {
           agent any
               environment {
                   //VOLUME = '$PWD/sources:/src'
                   IMAGE = 'pypi/twine:latest'
               }
               steps {
                   dir(path: env.BUILD_ID) {
                       unstash(name: 'app-content')
                       //unstash(name: 'setUpPy')
                       //unstash(name: 'pypirc')
                       //unstash(name: 'procfile')
                       //unstash(name: 'managePy')
                       //https://docs.python.org/3/distutils/builtdist.html
                       //sh 'cd sources'
                       sh 'ls -l'
                       //sh 'python3 setup.py bdist_dumb --format=zip'
                       //sh 'python3 setup.py sdist bdist_wheel'
                       //sh 'python3 -m twine upload -r nexus-pypi dist/* --config-file .pypirc --verbose'

                       sh 'cd ..'
                       sh 'wget -q -O - https://packages.cloudfoundry.org/debian/cli.cloudfoundry.org.key | sudo apt-key add -'
                       sh 'echo "deb https://packages.cloudfoundry.org/debian stable main" | sudo tee /etc/apt/sources.list.d/cloudfoundry-cli.list'
                       sh 'sudo apt-get update'
                       sh 'sudo apt-get install cf8-cli'
                       sh 'sudo apt-get install python3-django'

                       sh 'cf --help'
                       //sh 'cf login -a https://api.cf.us10.hana.ondemand.com/ -u mohtadi.nasri@focus-corporation.com -p 93407130Nm2021'
                       sh 'cf login -a https://api.cf.us10.hana.ondemand.com/ -u nadim.mabrouk@focus-corporation.com -p NADmab13446526='
                       sh 'cf create-route cfapps.us10.hana.ondemand.com --hostname my_app_django_a'
                       sh 'cf push my_app_django_a -b https://github.com/heroku/heroku-buildpack-python.git'

                    }
               }

        }
    }
}
