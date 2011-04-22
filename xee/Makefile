#
#   Copyright 2009 Joe Block <jpb@ApesSeekingKnowledge.net>
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.
#
#  Author:  Brent B
#  Created: 2011/04/21
#  Last Modified: 2011/04/21
#
#  Description:  This Makefile will download the version of Xee specified
#    in the PACKAGE_VERSION variable from Dag Agren's Google Code site,
#    unzip it, and package it.  Example of a zipped application.
#
include /usr/local/share/luggage/luggage.make


TITLE=Xee
REVERSE_DOMAIN=cx.c3.wakaba
PACKAGE_VERSION=2.2
PACKAGE_MAJOR=2
PACKAGE_MINOR=2

# Using a trick from ArchLinux Build System scripts: use the variables to build the source URL
APPZIP_LOCATION="http://xee.googlecode.com/files/${TITLE}${PACKAGE_VERSION}.zip"
#Space workaround
Xee.zip:
	curl ${APPZIP_LOCATION} -o Xee.zip
	
PAYLOAD=unzip-applications-Xee
