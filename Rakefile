require './constants.rb'

desc 'create a raw GeoJSON Text Sequence cache'
task :cache do
  sh <<-EOS
ruby ../yasumasa/yasumasa.rb > #{$cache_path}
  EOS
end

desc 'create PMTiles'
task :tiles do
  sh <<-EOS
tippecanoe -o tiles.mbtiles -f \
--minimum-zoom=#{$minzoom} --maximum-zoom=#{$maxzoom} \
--base-zoom=#{$maxzoom} \
--layer=#{$layer} #{$cache_path}; \
pmtiles convert tiles.mbtiles docs/tiles.pmtiles; \
rm tiles.mbtiles
  EOS
end

desc 'build style.json'
task :style do
  sh <<-EOS
charites build style.yml docs/style.json
  EOS
end

desc 'host the site'
task :host do
  sh <<-EOS
budo -d docs
  EOS
end

