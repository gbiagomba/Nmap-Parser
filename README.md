# Nmap-Parser
Parse nmap scan data with perl.

This module implements a interface to the information contained in an nmap scan. It is implemented by parsing the xml scan data that is generated by nmap. This will enable anyone who utilizes nmap to quickly create fast and robust security scripts that utilize the powerful port scanning abilities of nmap.

The latest version of this module can be found on here [http://modernistik.github.com/Nmap-Parser/](http://modernistik.github.com/Nmap-Parser/)

### Code Status
[![CPAN version](https://badge.fury.io/pl/Nmap-Parser.svg)](https://badge.fury.io/pl/Nmap-Parser)
[![Build Status](https://travis-ci.org/modernistik/Nmap-Parser.svg?branch=master)](https://travis-ci.org/modernistik/Nmap-Parser)

## Overview
Here is a small example on how to use the module. You can view the more detailed API and examples in the POD documentation.

```perl
    use Nmap::Parser;
    my $np = new Nmap::Parser;

    $np->parsescan($nmap_path, $nmap_args, @ips);
    #or
    $np->parsefile($file_xml);

    my $session    = $np->get_session();
    my $host       = $np->get_host($ip_addr);
    my $service = $host->tcp_service(80);
    my $os         = $host->os_sig();
```

Another method is to setup callbacks for each section.

```perl
    my $np2 = new Nmap::Parser;

    $np2->callback(\&my_callback);

    $np2->parsefile($file_xml);
    #or
    $np2->parsescan($nmap_path, $nmap_args, @ips);

    sub my_callback {
	    my $host = shift; #Nmap::Parser::Host object
    	#.. see documentation for all methods ...
    }
```   

## CPAN Installation (recommended)
The easiest way to install a Perl module is to use span. Run this in the command prompt to install directly from CPAN (may need root priviledges):

```bash
	$ perl -MCPAN -e 'install Nmap::Parser'
	# or cpan bin
	$ cpan install Nmap::Parser
```

## Manual Install
Download the file and unpack. This is usually done by:

	$ tar zxvf Nmap-Parser-x.xx.tar.gz

Where x.xx is the version number. Next change into the newly created directory. To install this module type the following:

  $ cpanm --quiet --installdeps --notest .
	$ perl Makefile.PL
	$ make
	$ make test
	$ make install

If you would like to install Nmap-Parser in a different directory (or if you do
not have root access use `perl Makefile.PL PREFIX=/install/path`, where
`/install/path` is the directory in which you want to install the module. Note
that you should then use the "use lib '/install/path'" in your scripts.


## ActiveState Perl (Windows only)
To install it on Windows, you may need to have installed the ActiveState Perl Package Manager (PPM). Run this in the command prompt:

	ppm install Nmap-Parser

This should contact the ActiveState respository, download the file and install it automagically.

### Dependencies
This module requires these other modules and libraries:

* XML::Twig 3.16+
* Storable (comes with Perl 5+)

In addition, you will need nmap 3.00+. You don't exactly need it, but this
version of nmap supports the xml output that this module can parse. So, you do
not really need the executable, but the xml output that you will be parsing
(or able to parse), must be from this version onward.

### Issues, Bugs and Feature Requests
Please submit any bugs or feature requests to: [https://github.com/modernistik/Nmap-Parser/issues](https://github.com/modernistik/Nmap-Parser/issues)

Please make sure that you submit the xml-output file of the scan which you are having
trouble with. This can be done by running your scan with the `-oX filename.xml` nmap switch. Please remove any important IP addresses for security reasons. It saves time in reproducing issues.

### Copyright and License
Copyright (C) 2003-2016 Anthony Persaud [http://www.modernistik.com](http://www.modernistik.com)

MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
