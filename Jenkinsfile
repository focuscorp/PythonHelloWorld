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
               sh 'wget -q -O - https://packages.cloudfoundry.org/debian/cli.cloudfoundry.org.key | sudo apt-key add -'
               sh 'echo "deb https://packages.cloudfoundry.org/debian stable main" | tee /etc/apt/sources.list.d/cloudfoundry-cli.list'
               sh 'sudo apt-get update'
               sh 'sudo apt-get install cf8-cli'
               //sh 'sudo apt-get install python3-django'

               sh 'cf --help'
               //sh 'cf login -a https://api.cf.us10.hana.ondemand.com/ -u mohtadi.nasri@focus-corporation.com -p 93407130Nm2021'
               sh 'cf login -a https://api.cf.us10.hana.ondemand.com/ -u nadim.mabrouk@focus-corporation.com -p NADmab13446526='
               sh 'cf apps'
               //sh 'cf create-route cfapps.us10.hana.ondemand.com --hostname my_app_django_'
               sh 'cf push'
          }
       }
    }
}
