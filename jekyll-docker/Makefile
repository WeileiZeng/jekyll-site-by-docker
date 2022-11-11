#port forwarding:
#ssh -L 8080:localhost:4000 weileizeng@10.101.4.63
#then visit localhost:8080 on your local machine to check the living site



#site_name=jekyll-site-by-docker-2
site_name=my-blog5
site_folder=$(PWD)/../docs
jekyll_folder=$(PWD)
#JEKYLL_VERSION=3.8
JEKYLL_VERSION=stable

info:
	echo current folder: $(PWD)
	echo site folder: $(site_folder)


new-site:
	echo edit site-name and run ./new-site.sh 
	echo then mv $(site_name) ../docs


#The following command runs in site_folder 
cmd=docker run --rm \
  --name="build-$(site_name)" \
  --volume="$(jekyll_folder):/srv/jekyll:Z" \
  --volume="$(jekyll_folder)/cache_vendor/$(site_name)/vendor/bundle:/usr/local/bundle:Z" \
  -e JEKYLL_UID="1011" \
  -e JEKYLL_GID="1011" \
  -it jekyll/jekyll:$(JEKYLL_VERSION)


bundle-install:
	cd $(site_folder) && $(cmd) bundle install
#	./run.sh 

#&& jekyll new jekyll-site-by-docker\""
build:
	echo add local-build/ in _config.yml exclude
	cd $(site_folder) && pwd && $(cmd) jekyll build --destination $(site_folder)/local-build/ --baseurl /$(site_name)/local-build --trace
serve:
	$(cmd) --publish [::1]:4000:4000 jekyll serve --port 4000 --incremental


