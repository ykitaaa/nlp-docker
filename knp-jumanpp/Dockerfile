#   Copyright [2018] [Kurohashi-Kawahara lab, Kyoto University]
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

FROM tennen/nlp-docker:jumanpp AS jumanpp

FROM tennen/nlp-docker:knp AS knp

FROM ruby:2.5.3-alpine3.8

# move to home
WORKDIR /

# jumanpp binary and scripts to main docker
COPY --from=jumanpp /usr/local .
# knp binary to main
COPY --from=knp /usr/local .

CMD ["jumanpp | knp"]
