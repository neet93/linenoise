require 'rake/clean'

$verbose = true

PREFIX = '/home/mav7/.local'
INCLUDE_PATH = "#{PREFIX}/include/linenoise" 
LIB_PATH = "#{PREFIX}/lib" 
PKG_PATH = "#{LIB_PATH}/pkgconfig"

OBJECT_EXTNAME = '.o'
LIB_EXTNAME = '.so'
PKG_EXTNAME = '.pc'

CC = 'cc'
CFLAGS = '-Wall -Werror -fpic'
LDDFLAGS = '-shared'
SOURCES = %w(linenoise.c example.c)
INCLUDES = %w(linenoise.h)
BINS = ["liblinenoise#{LIB_EXTNAME}", 'example']

PKG = "linenoise#{PKG_EXTNAME}"

desc 'Compiles, and links the source code'
task :all do
    sh "#{CC} #{CFLAGS} -c #{SOURCES.first}"
    sh "#{CC} #{LDDFLAGS} -o #{BINS.first} *#{OBJECT_EXTNAME}"
    sh "#{CC} #{CFLAGS} -o #{BINS.last} #{SOURCES.join(' ')}"
end

desc 'Compiles, and links the source code into a dynamic library'
task :build do
    sh "#{CC} #{CFLAGS} -c #{SOURCES}"
    sh "#{CC} #{LDDFLAGS} -o #{BINS.first} *#{OBJECT_EXTNAME}"
end

task default: :all

CLEAN.include("*#{OBJECT_EXTNAME}")
CLOBBER.include(BINS)

desc 'Self explanatory...'
task :install do
    FileUtils.mkdir(INCLUDE_PATH, verbose: $verbose) unless File.exist?(INCLUDE_PATH)
    FileUtils.mkdir(LIB_PATH, verbose: $verbose) unless File.exist?(LIB_PATH)

    INCLUDES.each do |e|
        FileUtils.cp(e, INCLUDE_PATH, verbose: $verbose)
    end
    FileUtils.cp(BINS.first, LIB_PATH, verbose: $verbose)
    FileUtils.cp(PKG, PKG_PATH, verbose: $verbose)
end

desc 'Remove install files(leaves behind made directories).'
task :uninstall do
    INCLUDES.each do |e|
        FileUtils.rm("#{INCLUDE_PATH}/#{e}", verbose: $verbose)
    end

    FileUtils.rm("#{LIB_PATH}/#{BINS.first}", verbose: $verbose)
    FileUtils.rm("#{PKG_PATH}/#{PKG}", verbose: $verbose)
end
