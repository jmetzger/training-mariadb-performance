# Setup training data contributions 

## Walkthrough (Debian/Ubuntu)

  * Complete process takes about 10 minutes 

```bash 
cd /usr/src; 
apt update; apt install git; 
git clone https://github.com/jmetzger/dedupe-examples.git;
cd dedupe-examples; 
cd mysql_example; 
# Eventually you need to enter (in mysql_example/mysql.cnf)  
# Only necessary if you cannot connect to db by entering "mysql" 
# password=<your_root_pw> 
./setup-debian.sh 
```

## Walkthrough (Redhat/Rocky) 

```bash 
cd /usr/src;
dnf install -y git 
git clone https://github.com/jmetzger/dedupe-examples.git;
cd dedupe-examples; 
cd mysql_example; 
# Eventually you need to enter (in mysql_example/mysql.cnf)  
# Only necessary if you cannot connect to db by entering "mysql" 
# password=<your_root_pw> 
./setup-rhel.sh 
```


