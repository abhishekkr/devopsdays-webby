#!rake
#

require 'rubygems'
require 'rake'
require 'fileutils'
require 'erb'

$WEBBYROOT = File.expand_path File.dirname(__FILE__)

namespace :proposal do

  # rake proposal:add event='2013-india' title='All About!' speaker='eve' type="ignite"
  desc "event='2121-india' title='All About!' speaker='eve' type='ignite' ## adds proposals"
  task :add do
    eventdir = File.join $WEBBYROOT, 'site', 'content', 'events', ENV['event']
    proposaldir = File.join eventdir, 'proposals', ENV['title']
    mkdir_p(proposaldir) unless File.directory? proposaldir
    unless ENV['EDITOR']
      puts 'Environment doesn\'t have EDITOR set.'
      exit 1
    end if

    template_file = File.join($WEBBYROOT, 'site', 'templates',
                        'base', 'proposals.erb')
    template_data = File.open(template_file, 'r') {|f| f.read() }
    @talk_type = ENV['type'] || 'talk'
    @talk_title = ENV['title']
    @talk_speaker = ENV['speaker'] || "anonymous"
    rendered_view = ERB.new(template_data)
    File.open(File.join(proposaldir, 'index.txt'), 'w') do |f|
      f.write(rendered_view.result(binding))
    end
    system("#{ENV['EDITOR']} \"#{File.join proposaldir, 'index.txt'}\"")
  end
end
