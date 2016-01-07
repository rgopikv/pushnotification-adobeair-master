# pushnotification-adobeair
Adobe Flex / AIR, mobile application should have .ane to implement push notification for android. Using .ane, we can able to get notifications from GCM.

This project helps to implement push notification styles like simple, bigPicture, and bigText. And,here also have support to generate new .ane file with the preferred notification  image.

- [x] To change notification image

  path to android/res/

  here we have

		drawable-hdpi/notify.png 
		drawable-ldpi/notify.png 
		drawable-mdpi/notify.png 
		drawable-xhdpi/notify.png 
   
   Replace custom image with the appropriate resolution.

- [x] generate .ane with changed image

	> path/to/flex/sdk/bin/adt.bat -package -target ane gcm.ane extension.xml -swc extension.swc -platform Android-ARM -C android .
	
	This will generates .ane file where you ran it.

- [x] if your want to generate it in a specified directory mention id at end

    > Eg:
    	-package -target ane gcm.ane extension.xml -swc extension.swc -platform Android-ARM -C android /destination/path/here

- [x] copy the .ane file and add it to your project.

- [x] make this app descriptor file changes in the android block.

				<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
				<uses-permission android:name="android.permission.INTERNET" />
				<permission android:name="YOUR_APP_ID_HERE.permission.C2D_MESSAGE" android:protectionLevel="signature" />
				<uses-permission android:name="YOUR_APP_ID_HERE.permission.C2D_MESSAGE" />
					    																																																																																																																																																																																							
			    <uses-feature android:required="false" android:name="android.hardware.wifi"/>
			         
					<application android:enabled="true" android:hardwareAccelerated="true"> 
						<service android:name="com.afterisk.shared.android.gcm.GCMIntentService" />
					
						<receiver android:name="com.afterisk.shared.android.gcm.AfteriskGCMBroadcastReceiver" 
							android:permission="com.google.android.c2dm.permission.SEND" >

							<intent-filter>
								<action android:name="com.google.android.c2dm.intent.RECEIVE" />
								<action android:name="com.google.android.c2dm.intent.REGISTRATION" />
								<category android:name="YOUR_APP_ID_HERE" />
							</intent-filter>
							
						</receiver>
		                <activity android:excludeFromRecents="false"> 
							<intent-filter> 
								<action android:name="android.intent.action.MAIN"/> 
								<category android:name="android.intent.category.LAUNCHER"/> 
	                        </intent-filter>	                
	                        
	                        <intent-filter>  
        						<action android:name="android.intent.action.SEND" />  
        						<category android:name="android.intent.category.DEFAULT" />  
        						<data android:mimeType="text/plain" />  
    						</intent-filter>  
    							
							<intent-filter> 
								<action android:name="android.intent.action.VIEW"/> 
								<category android:name="android.intent.category.BROWSABLE"/> 
								<category android:name="android.intent.category.DEFAULT"/> 
								<data android:scheme="kbrapp"/> 
								<data android:host="franchiseindia" />
							</intent-filter> 
		                  </activity> 


- [x] push message configurations

   If you using PHP script to push your notifications, follow these message array format for supporting all notification types.

``` PHP
$msg = array
(
    'message'       => 'message',
    'alert'         => 'alert',
    'imageurl'      => 'url/for/image/notification',
    'largeicon'     => 'icon/path/for/large/icon', size 72x72 or below
    'title'         => 'title',
    'subtitle'      => 'This is a subtitle',
    'tickerText'    => 'Ticker text here',
    'bigtext'        => 'text/paragraph/message/to/show/in/the/notification/drawer',
    'type'           => 'picture/bigText',
    'vibrate'   => 1 / 0,
    'sound'     => 1 / 0
);

```   			