# Bees with Machine Guns!

A utility for arming (creating) many bees (micro EC2 instances) to attack (load test) targets (web applications).

Also, retribution for "this shameful act":http://kottke.org/10/10/tiny-catapult-for-throwing-pies-at-bees against a proud hive.

## Dependencies

* Python 2.6
* boto
* paramiko

## Installation

```
git clone https://github.com/joystickinteractive/beeswithmachineguns
cd beeswithmachineguns
pip install -r requirements.txt
```

Put bees on your `$PATH` in order to use it from any directory. 

## Configuring AWS credentials

Bees uses boto to communicate with EC2 and thus supports all the same methods of storing credentials that it does.  These include declaring environment variables, machine-global configuration files, and per-user configuration files. You can read more about these options on "boto's configuration page":http://code.google.com/p/boto/wiki/BotoConfig.

At minimum, create a .boto file in your home directory with the following contents:

```
[Credentials]
aws_access_key_id = <your access key>
aws_secret_access_key = <your secret key>
```

The credentials used must have sufficient access to EC2.

Make sure the .boto file is only accessible by the current account:

```
chmod 600 .boto
```

h2. Usage

A typical bees session looks something like this:

```
bees up -s 4 -g public -k frakkingtoasters
bees attack -n 10000 -c 250 -u http://www.ournewwebbyhotness.com/
bees down
```

This spins up 4 servers in security group 'public' using the EC2 keypair 'frakkingtoasters', whose private key is expected to reside at ~/.ssh/frakkingtoasters.pem.

*Note*: the default EC2 security group is called 'default' and by default it locks out SSH access. I recommend creating a 'public' security group for use with the bees and explicitly opening port 22 on that group.

It then uses those 4 servers to send 10,000 requests, 250 at a time, to attack OurNewWebbyHotness.com.

Lastly, it spins down the 4 servers.  *Please remember to do this*--we aren't responsible for your EC2 bills.

For complete options type:

```
bees -h
```

## Bugs

Please log your bugs on the "Github issues tracker":http://github.com/newsapps/beeswithmachineguns/issues.

## Credits

The bees are a creation of the News Applications team at the Chicago Tribune--visit "our blog":http://apps.chicagotribune.com/ and read "our original post about the project":http://blog.apps.chicagotribune.com/2010/07/%2008/bees-with-machine-guns/.

Initial refactoring code and inspiration from "Jeff Larson":http://github.com/thejefflarson.

Thanks to everyone who reported bugs against the alpha release.

## License

MIT.
