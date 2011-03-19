
require 'set'

# automaticlly create all tags pages.
# return nil

def auto_create_tag
	
	get_tags.each do |tag|
		@items << Nanoc3::Item.new(
		"<%= render 'tag', :tag => '#{tag}' %>",
	  { :title => "Category: #{tag}", :is_hidden => true, :tag => "#{tag}"}, # do not include in sitemap.xml
	  "/tags/#{tag}/",                                     # identifier
	  :binary => false
	)

	end
	nil
end

# get all the tags of all articles.
# return the all tags array.

def get_tags
	tags = Set.new
	@site.articles.each do |post|
		if(post[:tags].nil?) 
			post[:tags] = Array.new
			post[:tags] << "(none)"
			tags << "(none)"
		else
			post[:tags].each do |tag|
				tags << tag
			end
		end
	end
	tags.to_a
end

# make all link tags of item
# return tag string of links(html code)

def make_tags(item)
	tags_for(item, { :base_url => @site.config()[:base_url] + "/tags/" })
end

# create all tags list
# return a string of html code, which is the tags list.

def make_tags_list
	tag_links = String.new
	get_tags.each do |tag|
		tag_links += "<li> + " + link_for_tag(tag, @site.config()[:base_url] + "/tags/") + " (#{items_with_tag(tag).count.to_s})</li>"
	end
	tag_links
end

# get the link of item by :kind
# return the link of item.

def link_of_item(kind)
	item = @items.find { |i| i.attributes()[:kind] == kind }
	link_to(kind.capitalize, @site.config()[:base_url] + item.path) unless item.nil?
end

