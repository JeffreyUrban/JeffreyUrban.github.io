---
title: SaltStack
---

Salt  
 Benefits \(vs Puppet and Chef\):  
  Can support agent-less configuration  
 Benefits \(vs Ansible, Puppet and Chef\):  
  Supports event-driven automation

SaltStack (salt)
	Install on master
		`curl -L https://bootstrap.saltstack.com -o install_salt.sh`
		`sudo sh install_salt.sh -P -M`  # -M for master
	Install on minion
		`sudo vim /etc/hosts`
			Add: `salt <master-ip>`
		`curl -L https://bootstrap.saltstack.com -o install_salt.sh`
		`sudo sh install_salt.sh -P`
	Provide master key to minion
		Master:
			`sudo salt-key -F master`  # Copy master.pub
		Minion:
			`sudo vim /etc/salt/minion`
				Set: `master_finger: ''<master.pub-key>'`
			`sudo systemctl restart salt-minion`
			`sudo salt-call --local key.finger`
				# Check local key fingerprint to compare against master unaccepted keys
		Master:
			`sudo vim /etc/salt/minion`
				Set: `master_finger: ''<master.pub-key>'`
			`sudo salt-call --local key.finger`
				# Check local key fingerprint to compare against master unaccepted keys
			`sudo salt-key -A`  # Accept keys (first, ensure they match)
			`sudo systemctl restart salt-minion`
	Run command on targets
		`salt '*' cmd.run "<command-line>" runas=<user>`
	Run command locally on a minion
		`salt-call --local cmd.run "<command-line>" runas=<user>`
	Selecting targets
	 	`salt <target-selector> <command> [<argument(s)>]`
		Target selectors:
			ID: `<id> or '<id>'`
			Grain: `-G '<grain>'`, e.g. `-G 'os:Ubuntu'`
			Regex: `'<regex>'`, e.g. `'*'`
			Compound: `-C '<compound-expression>'`, e.g. `'G@os:Ubuntu or E@db*'`
			List: `-L '<first>,<second>,...'`
	View available modules
		`salt 'salt' sys.list_modules`
	View functions within modules
		`salt 'salt' sys.list_functions <module>`
	View functions for a state module
		`salt '<target>' sys.list_state_functions <statemodule>`
	Documentation
		`salt 'salt' sys.doc <module>`
		`salt 'salt' sys.doc <function>`
	Test individual state(s)
		`salt '<target>' state.sls <state> test=true`
	Run individual state(s)
		`salt '<target>' state.sls <state>`
	Run modules
		`salt '<target>' state.apply <comma-delimited-list-of-modules-without-sls>`
	`top.sls`
		Maps which servers use which states
		Located at top of `file_roots` directory, or per `/etc/salt/master`, `state_top`.
		'Highstating' runs all modules listed in `top.sls` on relevant minions
	State files:
		Server root:
			`salt://` means server root, e.g. `/srv/salt/`
		Requisites (review these again... LA explanations don't make sense to me)
			`require`
				requires specified to run first
			`watch`
				if specified runs, it runs
			`watch_in`
				?
			`prereq`
				run `test=true` on targeted state
				if targeted state will make changes, dependent state runs first
			`onfail`
				if targeted fails, dependent runs
			`onchanges`
				if targeted makes changes, dependent runs
			`use`
				parameters of targeted used by dependent (except requisites)
		`module.wait`
			Don't run until triggered (such as by `watch` requisite)
	Grains
		Find minion OS family:
			`salt '*' grains.fetch os_family`
	Jinja
		Call a salt function
			`salt[<module>.<function>]('<parameters>')`
			`salt.<module>.<function>('<parameters>')`
		Set a variable based on a grain value
			Scope
				State-scope:
					Defined in `sls` file
				Formula-scope:
					Defined in `map.jinja` file
					Imported in `sls` file as
{% raw %}
						`{% from "<formula>/map.jinja" import <set> with context %}`
{% endraw %}
			example:
```
{% raw %}
				# Set variable 'package' in dictionary 'apache'
				{% set apache = salt['grains.filter_by']({
				'Debian': { 'package': 'apache2' },
				'RedHat': { 'package': 'httpd' },
				}) %}
				# Use variable
				{{ apache.package }}
{% endraw %}
```
		Variables (formula-scale)
			`map.jinja`

`saltbox`
	Prepend salt command-lines with:
		`saltbox exec -- <command-line>`

Saltstack Custom "execution module"
{% raw %}
	Something you can call from inside the jinja as {{ salt['foo.bar'](args....) }}
{% endraw %}
	it's basically just a .py file with a couple of special functions
	If you do happen to need to write one, note https://docs.python.org/3/library/ipaddress.html#ipaddress.IPv4Network.hosts

