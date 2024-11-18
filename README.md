Instalar Ansible:
```bash
sudo dnf install ansible -y
```

clonar el proyecto:
```bash
git clone https://github.com/HackCTF/ssh_secure_project.git
```

Ejecutar el playbook:
```bash
ansible-playbook playbooks/setup.yml
```

Entrar al sitio web mediante el navegador web
```bash
{{ ip_host }}:8080
```
