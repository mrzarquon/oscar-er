This is an Oscar environment for ER testing work.

This assumes you are using the latest oscar and vagrant (install from package, not the gem, weirdo).

It is 6 boxes. Don't even try this on battery (or with a machine on your lap)

vagrant up --provider=(virtualbox|vmware\_fusion)

(ensure all /etc/hosts are reprovisioned)
vagrant provision

(make sure you don't have to rebuild post testing)
vagrant plugin install multiprovider-snap
vagrant snap take

(reset / roll back)

vagrant snap rollback

To have these hosts in your /etc/hosts file, run something like this:
vagrant hosts puppetize | sudo puppet apply

If you are using fabric, what I had to do to get the vagrant key to work was explicity call the key and user, even after modifying my ~/.ssh/config

alias fab='fab -i ~/.vagrant/insecure_private_key -u vagrant'

should work without issue, example ssh config (in case to nerd snipe someone into fixing mine):

Host \*.puppetlabs.demo
  StrictHostKeyChecking no
  UserKnownHostsFile /dev/null
  ForwardAgent yes
  ForwardX11 no
  User vagrant
  IdentityFile /Users/cbarker/.ssh/insecure_private_key

