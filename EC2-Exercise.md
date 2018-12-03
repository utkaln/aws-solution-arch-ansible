#To create an EC2 instance from CLI we would need to create Security Group and Key pair created before we can start creating an instance

#Create key pair

```aws ec2 create-key-pair --key-name ec2-learn```


#Create Security Group

```aws ec2 create-security-group --group-name Utkal-ec2-sg1-cert-exam-cli --description "Utkal-ec2-sg1-cert-exam-cli"```

#Describe Security Group that just got created

```aws ec2 describe-security-groups --group-names Utkal-ec2-sg1-cert-exam-cli```


#Add rule to Security Group

```aws ec2 authorize-security-group-ingress --group-name Utkal-ec2-sg1-cert-exam-cli --protocol tcp --port 22 --cidr 0.0.0.0/0```



#Launch EC2 instance

```aws ec2 run-instances --image-id ami-09479453c5cde9639 --security-group-ids sg-02270386c0356280f --count 1 --instance-type t2.micro --key-name ec2-learn ```

#check status of EC2 instance
```aws ec2 describe-instance-status --instance-id i-0742114273af1b5cf```

#Create Tags in EC2 instance
```aws ec2 create-tags --resources i-0742114273af1b5cf --tags Key=Name,Value=Ec2-test-instance-cli Key=Name,Value=Ec2-test-instance-cli Key=Email,Value=nayak.utkal@gmail.com```



![alt text](https://github.com/utkaln/aws-solution-arch-ansible/blob/master/Screen%20Shot%202018-12-01%20at%207.47.19%20PM.png)
