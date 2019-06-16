#! /usr/bin/env ruby

require 'erb'
require 'rake/clean'
require 'securerandom'

TESTING_DIRECTORY   = "/tmp/var/www/"                               # Directory for testing phone number replacements
HTML_TEMPLATES      = Rake::FileList["templates/page_*"]            # Different HTML Template Files
SAMPLE_FILES        = Rake::FileList[TESTING_DIRECTORY + '/*']      # Look for Rendered Template files to Clean
BACKUP_FILES        = Rake::FileList['/tmp/backup/www/*']           # Look for Backup files

## Sampling of possible Phone number presentations ##
ORG_PHONE_NUMBERS   = ['800 438-4357','1 (800) 438-4357','1-800-438-4357','800.438.4357',
    '1.800.438.4357','1 (800) 438.4357','800-GET-HELP','1-800-GET-HELP','1 (800) GET-HELP']

class SampleHtmlPage

    def initialize(template: nil, phone_number: nil)
        @template       = File.read(template)
        @phone_number   = phone_number
    end

    ## Render the ERB into a string ##
    def render() ERB.new(@template, nil, '-').result( binding ) end

end

task :make_sample_files do

    mkdir_p TESTING_DIRECTORY

    10000.times do |i|

        html_template   = HTML_TEMPLATES.sample                 # Choose 1 of the available templates
        sample_number   = ORG_PHONE_NUMBERS.sample              # Choose 1 of the available phone number samples
        phone_template  = 'templates/number_samples.html.erb'   # Path to list of HTML phone number presentations

        ## Select 1 of the HTML phone number presentations ##
        html_number     = SampleHtmlPage.new(
                                template: phone_template, phone_number: sample_number
                            ).render.split("\n").sample

        ## Create Random file path ##
        sample_file     = TESTING_DIRECTORY + "page-#{SecureRandom.hex}.html"

        ## Write out the sample files ##
        begin
          file = File.open(sample_file, "w")
          file.write(SampleHtmlPage.new(template: html_template, phone_number: html_number).render) 
        ensure
          file.close unless file.nil?
        end

        printf("\rRendering: %s %d", sample_file, (i + 1) )

    end

    puts

end

task :default => :make_sample_files

CLEAN.include(SAMPLE_FILES)
CLEAN.include(BACKUP_FILES)
CLOBBER << "/tmp/var"
CLOBBER << "/tmp/backup"