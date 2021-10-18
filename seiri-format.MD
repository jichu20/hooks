#!/bin/sh
#
# This hook will run the eclipse code formatter before any commit
# to make the source look as it's supposed to look like in the repo.

ECLIPSE_HOME="/Users/borja.sanchez/Code/utils/hooks/hook/"
STYLE_FILE="$HOME/seiriFormat.xml"
echo "Running pre-commit hook: run-eclipse-formatter---------------------"
echo "Will run eclipse formatter, using: $STYLE_FILE"
echo "Listing folders to run formatter on… "
code_dirs=`find . -maxdepth 3 | grep 'src/'`
for dir in $code_dirs; do
   echo $dir;
done;
      
echo "Launching eclipse code formatter…    "
exec $ECLIPSE_HOME/eclipse \
                    -nosplash \
                    -application org.eclipse.jdt.core.JavaCodeFormatter \
                    -verbose \
                    -config $STYLE_FILE \
                    $code_dirs

echo "done---------------------------------------------------------------"
