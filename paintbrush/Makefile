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
#  Created: 2011/07/12
#  Last Modified: 2011/07/12
#
#  Description:  This Makefile will download the version of Paintbrush specified
#    in the PACKAGE_VERSION variable from a Sourceforge mirror, 
#    unzip it, and package it.  Example of a zipped application.
#
include /usr/local/share/luggage/luggage.make


TITLE=Paintbrush
REVERSE_DOMAIN=net.sourceforge
PACKAGE_VERSION=2.1.1
PACKAGE_MAJOR=2
PACKAGE_MINOR=1

# Using a trick from ArchLinux Build System scripts: use the variables to build the source URL
# Note the directory structure

APPZIP_LOCATION="http://downloads.sourceforge.net/project/paintbrush/${TITLE}%20${PACKAGE_MAJOR}.x/${TITLE}%20${PACKAGE_VERSION}/${TITLE}-${PACKAGE_VERSION}.zip"
#Space workaround
Paintbrush.zip:
	curl -L ${APPZIP_LOCATION} -o Paintbrush.zip
	
PAYLOAD=unzip-applications-Paintbrush
