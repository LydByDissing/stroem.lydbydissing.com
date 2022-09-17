convertImages:
	$(shell find ./ -type f -name '*.jpg' -exec sh -c 'cwebp $1 -o "${1%.jpg}.webp"' _ {} \;)
	#find ./ -type f -name '*.png' -exec sh -c 'cwebp $1 -o "${1%.png}.webp"' _ {} \;

buildSite: convertImages
	bash -c "hugo -D
