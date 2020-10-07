# Android-Date-Time-Format
Format DateTime in Android


DateTime is a common utility in Android. These days most of the project required date and time formatting in Android. So we are building a plug and play solution. I hope each developer will keep this utility in own inbox for time-saving purpose. In this tutorial, we demonstrate different-different date formatting and parsing

SimpleDateFormat is a java class which extends the DateFormat java class. It is used for normalization, formatting and parsing date in a locale-sensitive manner.


SimpleDateFormat is used for below utility in Android
Formatting – It allows for formatting Date to Text in Android any given locale.
Parsing – You can parse any Text in Date object by using SimpleDateFormat
Some specific Letter is used to representing Date or Time Component in Android. You can read the Google Official site.

# Formatting
Here we discuss some date format my intention is to cover each combination of date format.

DATE_FORMAT_1 = hh:mm a
The output will be -: 10:37 am
 
DATE_FORMAT_2 = h:mm a
Output will be -: 10:37 am
 
DATE_FORMAT_3 = yyyy-MM-dd
The output will be -: 2018-12-05
 
DATE_FORMAT_4 = dd-MMMM-yyyy
The output will be -: 05-December-2018
 
DATE_FORMAT_5 = dd MMMM yyyy
The output will be -: 05 December 2018
 
DATE_FORMAT_6 = dd MMMM yyyy zzzz
The output will be -: 05 December 2018 UTC
 
DATE_FORMAT_7 = EEE, MMM d, ''yy
The output will be -: Wed, Dec 5, '18
 
DATE_FORMAT_8 = yyyy-MM-dd HH:mm:ss
The Output will be -: 2018-12-05 10:37:43
 
DATE_FORMAT_9 = h:mm a dd MMMM yyyy
The output will be -: 10:37 am 05 December 2018
 
DATE_FORMAT_10 = K:mm a, z
The output will be -: 10:37 am, UTC
 
DATE_FORMAT_11 = hh 'o''clock' a, zzzz
The output will be -: 10 o'clock am, UTC
 
DATE_FORMAT_12 = yyyy-MM-dd'T'HH:mm:ss.SSS'Z'
The output will be -: 2018-12-05T10:37:43.937Z
 
DATE_FORMAT_13 = E, dd MMM yyyy HH:mm:ss z
The output will be -: Wed, 05 Dec 2018 10:37:43 UTC
 
DATE_FORMAT_14 = yyyy.MM.dd G 'at' HH:mm:ss z
The output will be -: 2018.12.05 AD at 10:37:43 UTC
 
DATE_FORMAT_15 = yyyyy.MMMMM.dd GGG hh:mm aaa
The output will be -: 02018.D.05 AD 10:37 am
 
DATE_FORMAT_16 = EEE, d MMM yyyy HH:mm:ss Z
The output will be -: Wed, 5 Dec 2018 10:37:43 +0000
 
DATE_FORMAT_17 = yyyy-MM-dd'T'HH:mm:ss.SSSZ
The output will be -: 2018-12-05T10:37:43.946+0000
 
DATE_FORMAT_18 = yyyy-MM-dd'T'HH:mm:ss.SSSXXX
The output will be -: 2018-12-05T10:37:43.949Z
 
DATE_FORMAT_19 = dd-MMM-yyyy
The output will be -: 05-Dec-2018

All the above date format combinations. Now comes utility class.

# Get Current Date
Example 1
/**
 * Default date format 
 */
public static final String DATE_FORMAT_2 = "dd-MMM-yyyy";
 
public static String getCurrentDate() {
    SimpleDateFormat dateFormat = new SimpleDateFormat(DATE_FORMAT_1);
    dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
    Date today = Calendar.getInstance().getTime();
    return dateFormat.format(today);
}

# Get current Time
Example 2
/**
 * Default time format
 */
public static final String DATE_FORMAT_1 = "hh:mm a";
 
public static String getCurrentTime() {
    SimpleDateFormat dateFormat = new SimpleDateFormat(DATE_FORMAT_1);
    dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
    Date today = Calendar.getInstance().getTime();
    return dateFormat.format(today);
}

# Get Date and Time from Timestamp
Example 3
  /**
   * 
   * @param time in milliseconds (Timestamp)
   * @param mDateFormat SimpleDateFormat
   * @return
   */
  public static String getDateTimeFromTimeStamp(Long time, String mDateFormat) {
      SimpleDateFormat dateFormat = new SimpleDateFormat(mDateFormat);
      dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
      Date dateTime = new Date(time);
      return dateFormat.format(dateTime);
  }
  
# How to use it
  /**
   * Get current date example 1
   */
  String mCurrentDate = DateUtils.getCurrentDate();
  /**
   * Get current time example 2
   */
  String mCurrentTime = DateUtils.getCurrentTime();
  /**
   * Date Format example 3
   */
  public static final String DATE_FORMAT = "dd-MMM-yyyy";
  String mDateTime = DateUtils.getDateFromTimeStamp(System.currentTimeMillis(), DATE_FORMAT);


# Date Parsing in Android
Let’s take few examples of date parsing

# Get Timestamp from DateTime in Android
Example 4
  /**
   * Get Timestamp from date and time
   * @param mDateTime datetime String
   * @param mDateFormat Date Format 
   * @return
   * @throws ParseException
   */
  public static long getTimeStampFromDateTime(String mDateTime, String mDateFormat) throws ParseException {
    SimpleDateFormat dateFormat = new SimpleDateFormat(mDateFormat);
    dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
    Date date = dateFormat.parse(mDateTime);
    return date.getTime();
  }
# Get DateTime from Date instances
Example 5
/**
  * Return  datetime String from date object  
  * @param mDateFormat format of date 
  * @param date date object that you want to parse
  * @return
  */
 public static String formatDateTimeFromDate(String mDateFormat, Date date) {
     if (date == null) {
         return null;
     }
     return DateFormat.format(mDateFormat, date).toString();
 }


# Convert DateTime String to another DateTime String format
This is very useful and confusing utility in Android

Example 6
 /**
   * Convert one date format string  to another date format string in android
   *
   * @param inputDateFormat Input SimpleDateFormat
   * @param outputDateFormat Output SimpleDateFormat
   * @param inputDate input Date String
   * @throws ParseException
   */
  public static String formatDateFromDateString(String inputDateFormat, String outputDateFormat,
      String inputDate) throws ParseException {
    Date mParsedDate;
    String mOutputDateString;
    SimpleDateFormat mInputDateFormat =
        new SimpleDateFormat(inputDateFormat, java.util.Locale.getDefault());
    SimpleDateFormat mOutputDateFormat =
        new SimpleDateFormat(outputDateFormat, java.util.Locale.getDefault());
    mParsedDate = mInputDateFormat.parse(inputDate);
    mOutputDateString = mOutputDateFormat.format(mParsedDate);
    return mOutputDateString;
  }
  
# How to use
  /**
   * Date Format example 4
   */
  public static final String DATE_FORMAT = "yyyy-MM-dd HH:mm:ss";
  String mDateTimeString = "2018-12-05 10:37:43";
  try {
    long mTimestamp = DateUtils.getTimeStampFromDateTime(mDateTimeString, DATE_FORMAT);
  } catch (ParseException e) {
    e.printStackTrace();
  }
  /**
   * Get current datetime example 5
   */
  public static final String DATE_FORMAT = "yyyy-MM-dd HH:mm:ss";
  String mDateTime = DateUtils.formatDateTimeFromDate(DATE_FORMAT, Calendar.getInstance().getTime());
  /**  Example 6
   * DateTime Input Format
   */
  public static final String DATE_INPUT_FORMAT = "yyyy-MM-dd HH:mm:ss";
  /**
   * DateTime Output Format
   */
  public static final String DATE_OUTPUT_FORMAT = "dd-MMM-yyyy";
  String mDateTimeString = "2018-12-05 10:37:43";
  String mDateTime = null;
  try {
    mDateTime = DateUtils.formatDateFromDateString(DATE_INPUT_FORMAT, DATE_OUTPUT_FORMAT, mDateTimeString);
  } catch (ParseException e) {
    e.printStackTrace();
  }
  The output is - 05-Dec-2018;


# The complete utility seems like below

package com.androidwave.datetimeutils.utils;
 
import android.text.format.DateFormat;
 
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;
import java.util.TimeZone;
  public class DateUtils {
    private static final String TAG = "DateUtils";
    public static final String DATE_FORMAT_1 = "hh:mm a";
    public static final String DATE_FORMAT_2 = "h:mm a";
    public static final String DATE_FORMAT_3 = "yyyy-MM-dd";
    public static final String DATE_FORMAT_4 = "dd-MMMM-yyyy";
    public static final String DATE_FORMAT_5 = "dd MMMM yyyy";
    public static final String DATE_FORMAT_6 = "dd MMMM yyyy zzzz";
    public static final String DATE_FORMAT_7 = "EEE, MMM d, ''yy";
    public static final String DATE_FORMAT_8 = "yyyy-MM-dd HH:mm:ss";
    public static final String DATE_FORMAT_9 = "h:mm a dd MMMM yyyy";
    public static final String DATE_FORMAT_10 = "K:mm a, z";
    public static final String DATE_FORMAT_11 = "hh 'o''clock' a, zzzz";
    public static final String DATE_FORMAT_12 = "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'";
    public static final String DATE_FORMAT_13 = "E, dd MMM yyyy HH:mm:ss z";
    public static final String DATE_FORMAT_14 = "yyyy.MM.dd G 'at' HH:mm:ss z";
    public static final String DATE_FORMAT_15 = "yyyyy.MMMMM.dd GGG hh:mm aaa";
    public static final String DATE_FORMAT_16 = "EEE, d MMM yyyy HH:mm:ss Z";
    public static final String DATE_FORMAT_17 = "yyyy-MM-dd'T'HH:mm:ss.SSSZ";
    public static final String DATE_FORMAT_18 = "yyyy-MM-dd'T'HH:mm:ss.SSSXXX";
    public static String getCurrentDate() {
      SimpleDateFormat dateFormat = new SimpleDateFormat(DATE_FORMAT_1);
      dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
      Date today = Calendar.getInstance().getTime();
      return dateFormat.format(today);
    }
    public static String getCurrentTime() {
      SimpleDateFormat dateFormat = new SimpleDateFormat(DATE_FORMAT_1);
      dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
      Date today = Calendar.getInstance().getTime();
      return dateFormat.format(today);
    }
    /**
     * @param time in milliseconds (Timestamp)
     * @param mDateFormat SimpleDateFormat
     */
    public static String getDateTimeFromTimeStamp(Long time, String mDateFormat) {
      SimpleDateFormat dateFormat = new SimpleDateFormat(mDateFormat);
      dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
      Date dateTime = new Date(time);
      return dateFormat.format(dateTime);
    }
    /**
     * Get Timestamp from date and time
     *
     * @param mDateTime datetime String
     * @param mDateFormat Date Format
     * @throws ParseException
     */
    public static long getTimeStampFromDateTime(String mDateTime, String mDateFormat)
        throws ParseException {
      SimpleDateFormat dateFormat = new SimpleDateFormat(mDateFormat);
      dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
      Date date = dateFormat.parse(mDateTime);
      return date.getTime();
    }
    /**
     * Return  datetime String from date object
     *
     * @param mDateFormat format of date
     * @param date date object that you want to parse
     */
    public static String formatDateTimeFromDate(String mDateFormat, Date date) {
      if (date == null) {
        return null;
      }
      return DateFormat.format(mDateFormat, date).toString();
    }
    /**
     * Convert one date format string  to another date format string in android
     *
     * @param inputDateFormat Input SimpleDateFormat
     * @param outputDateFormat Output SimpleDateFormat
     * @param inputDate input Date String
     * @throws ParseException
     */
    public static String formatDateFromDateString(String inputDateFormat, String outputDateFormat,
        String inputDate) throws ParseException {
      Date mParsedDate;
      String mOutputDateString;
      SimpleDateFormat mInputDateFormat =
          new SimpleDateFormat(inputDateFormat, java.util.Locale.getDefault());
      SimpleDateFormat mOutputDateFormat =
          new SimpleDateFormat(outputDateFormat, java.util.Locale.getDefault());
      mParsedDate = mInputDateFormat.parse(inputDate);
      mOutputDateString = mOutputDateFormat.format(mParsedDate);
      return mOutputDateString;
    }
  }
