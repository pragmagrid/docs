

+ Original contents are from wordpress http://www.nsf-nsfc-sw.org
+ Method 1: use **jekyll** (did not work because of chinese characters in xml file)
    
  1. install jekyll, on MacOS  as root:
	 + gem install jekyll
	 + gem install jekyll-import
	 + gem install sequel
	 + gem install hpricot

  2. Export wp site from wordpress dashboard  as an xml file
     and save as nsf-nsfc/us-chinasoftwareworkshop.wordpress.2014-08-06.xml

  3. Try to convert pages :
	  + jekyll new nsf-nsfc
	  + cd nsf-nsfc/
	  + ruby -rubygems -e 'require "jekyll-import"; 
				 JekyllImport::Importers::WordpressDotCom.run({
				 "source" => "us-chinasoftwareworkshop.wordpress.2014-08-06.xml",
				 "no_fetch_images" => false, "assets_folder" => "assets" })'

     The conversion failes on non-latin characters

+ Method 2: use **exitwp**

  1. Download exitwp and its prerequisites. For python modules install as root 

     + git clone https://github.com/thomasf/exitwp
     + wget http://pyyaml.org/download/pyyaml/PyYAML-3.11.tar.gz
     + tar xzvf PyYAML-3.11.tar.gz 
     + cd PyYAML-3.11
     + python setup.py --without-libyaml build
     + python setup.py --without-libyaml install
     + wget http://www.crummy.com/software/BeautifulSoup/bs4/download/4.3/beautifulsoup4-4.3.2.tar.gz
     + tar xzvf beautifulsoup4-4.3.2.tar.gz 
     + cd beautifulsoup4-4.3.2
     + python setup.py build
     + python setup.py install

  2. Put saved export xml file from wordpress  in exitwp:
     + ls exitwp/
     + cp us-chinasoftwareworkshop.wordpress.2014-08-06.xml exitwp/wordpress-xml/
     + cd exitwp/
     + xmllint --noout wordpress-xml/us-chinasoftwareworkshop.wordpress.2014-08-06.xml 
     + python exitwp.py 
     
     The resulting md files are in exitwp/build/jekyll/www.nsf-nsfc-sw.org/
     Edit and consolidate as needed.

+ Download all images separately, none of methods dealt with images
+ Use http://markdownrules.com  to convert participants pages, none of the
  methods dealt with WP tables.  Edit resulting md files
+ Download presentations are goc.pragma-grid.net:/var/www/html/doc/CUSW*

  rm /var/www/html/doc/* on goc 
