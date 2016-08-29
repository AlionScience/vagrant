################################################################################
#
# Vagrantfile
#
################################################################################

# Buildroot version to use
RELEASE='2016.05'

### Change here for more memory/cores ###
VM_MEMORY=2048
VM_CORES=1

Vagrant.configure('2') do |config|
	config.vm.box = 'ubuntu/trusty64'

	config.vm.provider :vmware_fusion do |v, override|
		v.vmx['memsize'] = VM_MEMORY
		v.vmx['numvcpus'] = VM_CORES
	end

	config.vm.provider :virtualbox do |v, override|
		v.memory = VM_MEMORY
		v.cpus = VM_CORES

		required_plugins = %w( vagrant-vbguest )
		required_plugins.each do |plugin|
		  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
		end
	end

	config.vm.provision 'shell' do |s|
		s.inline = 'echo Setting up machine name'

		config.vm.provider :vmware_fusion do |v, override|
			v.vmx['displayname'] = "Buildroot #{RELEASE}"
		end

		config.vm.provider :virtualbox do |v, override|
			v.name = "Buildroot #{RELEASE}"
		end
	end

	config.vm.provision 'shell', inline:
		"sudo dpkg --add-architecture i386
		sudo apt-get -q update
		sudo apt-get -q -y install build-essential libncurses5-dev \
			git bzr cvs mercurial subversion libc6:i386 unzip
		sudo apt-get -q -y autoremove
		sudo apt-get -q -y clean"

	config.vm.provision 'shell', privileged: false, inline:
		"echo 'Downloading and extracting buildroot #{RELEASE}'
		wget -q -c https://github.com/bfrantz/buildroot/archive/master.tar.gz
		tar axf master.tar.gz
		mv buildroot-master buildroot-alion"

	config.vm.synced_folder "share/", "/home/vagrant/share"
end
