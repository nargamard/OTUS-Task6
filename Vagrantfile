ENV["LC_ALL"] = "en_US.UTF-8"
ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

# Описание параметров ВМ
MACHINES = {
  :rpmmaker => {
        :box_name => "centos/8",
        # Имя VM
        :vm_name => "rpmmaker",
        # Количество ядер CPU
        :cpus => 4,
        # Указываем количество ОЗУ (В Мегабайтах)
        :memory => 8096,
        # Указываем IP-адрес для ВМ
        :ip => "192.168.56.10",
  },
 }

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|
    
    config.vm.define boxname do |box|
   
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxconfig[:vm_name]
      box.vm.network "private_network", ip: boxconfig[:ip]
      box.vm.provider "virtualbox" do |v|
        v.memory = boxconfig[:memory]
        v.cpus = boxconfig[:cpus]
      end

     # Запуск ansible-playbook
      if boxconfig[:vm_name] == "rpmmaker"
       box.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/provision.yml"
        ansible.inventory_path = "ansible/hosts"
        ansible.host_key_checking = "false"
        ansible.limit = "all"
       end
      end
    end
  end
end
