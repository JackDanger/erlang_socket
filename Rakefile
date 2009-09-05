require 'rake/clean'

INCLUDE = "include"
vertest = `erl -noshell -eval 'io:format("~n~s~n", [erlang:system_info(otp_release)]).' -s erlang halt | tail -n 1`.chomp
if vertest =~ /(R\d\d[AB])/
	OTPVERSION = $1
else
	STDERR.puts "unable to determine OTP version! (I got #{vertest})"
	exit -1
end
ERLC_FLAGS = "-I#{INCLUDE} -D #{OTPVERSION} +warn_unused_vars +warn_unused_import +warn_exported_vars +warn_untyped_record"

SRC = FileList['src/*.erl']
OBJ = SRC.pathmap("%{src,ebin}X.beam")
DEBUGOBJ = SRC.pathmap("%{src,debug_ebin}X.beam")

# check to see if gmake is available, if not fall back on the system make
if res = `which gmake` and $?.exitstatus.zero? and not res =~ /no gmake in/
	MAKE = File.basename(res.chomp)
else
	MAKE = 'make'
end

@maxwidth = SRC.map{|x| File.basename(x, 'erl').length}.max

CLEAN.include("ebin/*.beam")
CLEAN.include("debug_ebin/*.beam")

verbose(true) unless ENV['quiet']

directory 'ebin'
directory 'debug_ebin'

rule ".beam" => ["%{ebin,src}X.erl"] do |t|
	sh "erlc -pa ebin -W #{ERLC_FLAGS} +warn_missing_spec -o ebin #{t.source} "
end

rule ".beam" => ["%{debug_ebin,src}X.erl"] do |t|
	sh "erlc +debug_info -D EUNIT -pa debug_ebin -W #{ERLC_FLAGS} -o debug_ebin #{t.source} "
  mod = File.basename(t.source, '.erl')
	sh "erl -noshell -pa debug_ebin -sname testpx -eval 'eunit:test(#{mod}, [verbose]).' -s erlang halt"
end


task :compile => 'ebin'

task :default => :compile

desc "Alias for test:all"
task :test => "test:all"

namespace :test do
	desc "Compile .beam files with -DEUNIT and +debug_info => debug_ebin"
	task :compile => ['debug_ebin'] + DEBUGOBJ

	desc "run eunit tests and output coverage reports"
	task :all => [:compile, :eunit]

	desc "run only the eunit tests"
	task :eunit => :compile
end
