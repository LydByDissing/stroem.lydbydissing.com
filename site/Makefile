JPEG_IMAGES := $(shell find ./ -type f -name '*.jpg')
PNG_IMAGES  := $(shell find ./ -type f -name '*.png')

convertImages: convertJpegImages convertPngImages

convertJpegImages:
	for i in $(JPEG_IMAGES); do \
		cwebp -mt $$i -o "$${i%.jpg}.webp";\
		avifenc --min 0 --max 63 --minalpha 0 --maxalpha 63 --advanced end-usage=q --advanced cq-level=32 --advanced tune=ssim --speed 0 --jobs all --ignore-icc $$i "$${i%.jpg}.avif";\
	done

convertPngImages:
	for i in $(PNG_IMAGES); do \
		cwebp -mt $$i -o "$${i%.png}.webp";\
		avifenc --min 0 --max 63 --minalpha 0 --maxalpha 63 --advanced end-usage=q --advanced cq-level=32 --advanced tune=ssim --speed 0 --jobs all --ignore-icc $$i "$${i%.png}.avif";\
	done

buildSite: convertImages
	bash -c "hugo -D --minify"

installDependencies:
	brew install hugo
	brew install webp
	brew install joedrago/repo/avifenc
