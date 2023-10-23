docs-install:
	gem install jekyll bundler
	bundle install --gemfile=Gemfile

# To run localy you need to use ruby version =< 2.7.6, but not >=3.x , see https://bbs.archlinux.org/viewtopic.php?pid=1976408#p1976408
#
# run local server for documentation website
# at http://127.0.0.1:4000/
# On first use, please run `make docs-install`
docs-up:
	JEKYLL_GITHUB_TOKEN=blank PAGES_API_URL=http://0.0.0.0 bundle exec \
		--gemfile=Gemfile \
	 	jekyll server --livereload

docs-up-docker:
	docker run --rm -it \
		-e JEKYLL_GITHUB_TOKEN=blank \
		-e PAGES_API_URL=http://0.0.0.0 \
		-e PAGES_REPO_NWO=VictoriaMetrics/VictoriaMetrics \
		-p 4000:4000 \
		-v $(PWD):/srv/jekyll \
		jekyll/jekyll:3.8 jekyll serve --livereload

# This commands is helpful when you want to convert image to the webp format
# All images quality set to 20% but it just reduce the size of image, but not the display quality

# To run image convertor just run next command in the terminal
#
# PATH_TO_IMAGES=path_to_the_images IMAGES_EXTENSION=png make docs-change-images
#
# This command will reduce all images with extionsion and folder defined in the command.
# All images with defined extensions will be removed.
# After that it is nesessary to update src attribute for image tag

docs-images-to-webp:
	docker run -it --rm -v \
		$(PWD)/$(PATH_TO_IMAGES):/data \
		elswork/cwebp \
		find ./ -type f -name '*.$(IMAGES_EXTENSION)' -exec sh -c 'cwebp -q 20 -m 6 $$1 -o "$${1%.png}.webp"' _ {} \;

docs-remove-old-images:
	rm -f $(PWD)/$(PATH_TO_IMAGES)/*.$(IMAGES_EXTENSION)

docs-change-images: \
	docs-images-to-webp \
	docs-remove-old-images
