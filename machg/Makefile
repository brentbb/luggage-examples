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
#  Created: 2011/06/09
#  Last Modified: 2011/06/09
#
#  Description:  This Makefile will download the version of MacHg specified
#    in the PACKAGE_VERSION variable from Jason Harris's site,
#    unzip it, and package it.  Example of a zipped application.
#
include /usr/local/share/luggage/luggage.make


TITLE=MacHg
REVERSE_DOMAIN=com.jasonfharris
PACKAGE_VERSION=0.9.23
PACKAGE_MAJOR=0
PACKAGE_MINOR=9

# Using a trick from ArchLinux Build System scripts: use the variables to build the source URL
APPZIP_LOCATION="http://jasonfharris.com/machg/downloads/assets/${TITLE}${PACKAGE_VERSION}.zip"
MacHg.zip:
	curl ${APPZIP_LOCATION} -o MacHg.zip
	
PAYLOAD=unzip-applications-MacHg
