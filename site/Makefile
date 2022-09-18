BREW := $(shell command -v brew)
HUGO := $(shell command -v hugo)
FIND := $(shell command -v find)
#SH   := $(shell command -v sh)

JPEG_IMAGES := $(shell find ./ -type f -name '*.jpg')
PNG_IMAGES  := $(shell find ./ -type f -name '*.png')

convertImages: convertJpegImages convertPngImages

convertJpegImages:
	for i in $(JPEG_IMAGES); do \
		cwebp $$i -o "$${i%.jpg}.webp";\
		avifenc --min 0 --max 63 --minalpha 0 --maxalpha 63 --advanced end-usage=q --advanced cq-level=32 --advanced tune=ssim --speed 0 --jobs 1 --ignore-icc $$i "$${i%.jpg}.avif";\
	done

convertPngImages:
	for i in $(PNG_IMAGES); do \
		cwebp $$i -o "$${i%.png}.webp";\
		avifenc --min 0 --max 63 --minalpha 0 --maxalpha 63 --advanced end-usage=q --advanced cq-level=32 --advanced tune=ssim --speed 0 --jobs 1 --ignore-icc $$i "$${i%.png}.avif";\
	done

buildSite: convertImages
	bash -c "hugo -D --minify"

installDependencies:
	$(BREW) install hugo
	$(BREW) install webp
	$(BREW) install joedrago/repo/avifenc
