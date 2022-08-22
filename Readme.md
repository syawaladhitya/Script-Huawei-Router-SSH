I hope this script could help you





      ___Syawal Adhita__




### TESTING SCRIPT For HUAWEI
import paramiko
import time


ssh_client = paramiko.SSHClient()
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh_client.connect(hostname='<your_ip_gateway>',username='admin',password='<credentialsdevice>')

conn = ssh_client.invoke_shell()


conn.send('system-view\n')
conn.send('interface loopback 0\n')
conn.send('ip add 10.10.10.10 255.255.255.255\n')
conn.send('quit\n')
conn.send('interface gigabitethernet0/0/0\n')
conn.send('ip add 192.168.9.10 255.255.255.0\n')
conn.send('quit\n')
conn.send('interface gigabitethernet0/0/2\n')
conn.send('ip add 192.168.6.1 255.255.255.0\n')
conn.send('quit\n')
conn.send('interface gigabitethernet0/0/2\n')
conn.send('ip add 192.168.3.1 255.255.255.0\n')
conn.send('quit\n')
conn.send('display ip interface brief\n')
conn.send('vlan 20\n')
conn.send('quit\n')
conn.send('vlan10\n')
conn.send('quit\n')
conn.send('interface vlanif 20\n')
conn.send('ip add 10.11.8.1 255.255.255.0\n')
conn.send('quit\n')
conn.send('interface vlanif 10\n')
conn.send('ip add 10.11.10.1\n')
conn.send('quit\n')

time.sleep(1)

output = conn.recv(65535)
print(output.decode('ascii'))

ssh_client.close()

