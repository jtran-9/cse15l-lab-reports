# Lab Report 3

# Part 1 - Bugs

I will be analyzing the Array Functions.

## Failure-inducing Inputs
Below is the test code that contains inputs that produces errors. The failure-inducing inputs are labeled with comments right next to them in the code below.
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {

  @Test 
  public void testReverseInPlace() {
    int[] input1 = { 3 };
    int[] input2 = {5, 7, 9}; // failure-inducing input
    int[] input3 = {1, 4, 6, 8}; // failure-inducing input
    ArrayExamples.reverseInPlace(input1);
    ArrayExamples.reverseInPlace(input2);
    ArrayExamples.reverseInPlace(input3);
    assertArrayEquals(new int[]{ 3 }, input1);
    assertArrayEquals(new int[] {9, 7, 5}, input2);
    assertArrayEquals(new int[] {8, 6, 4, 1}, input3);
  }


  @Test
  public void testReversed() {
    int[] input1 = { };
    int[] input2 = {0, 1, 2}; // failure-inducing input
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
    assertArrayEquals(new int[]{2, 1, 0}, ArrayExamples.reversed(input2));
  }
  
  @Test
  public void testAverageWithoutLowest() {
    double[] input1 = {1.0, 2.0, 3.0};
    double[] input2 = {1.0, 1.0, 2.0, 3.0}; // failure-inducing input
    assertEquals(2.5, ArrayExamples.averageWithoutLowest(input1), 0.0001);
    assertEquals(2.5, ArrayExamples.averageWithoutLowest(input2), 0.0001);
  }
    
}
```
I will list the failure-inducing inputs in this paragraph as well. For the testReverseInPlace() function, the failure-inducing inputs were [5, 7, 9] and [1, 4, 6, 8]. For the testReversed() functoin, the failure-inducing input was [0, 1, 2]. For the testAverageWithoutLowest() function, the failure-inducing input was [1.0, 1.0, 2.0, 3.0].

## NOT Failure-inducing Inputs
Below is the test code that contains inputs that does not produce errors. The inputs that do not cause errors are labeled with comments right next to them in the code below.
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {

  @Test 
  public void testReverseInPlace() {
    int[] input1 = { 3 }; // NOT failure-inducing input
    int[] input2 = {5, 7, 9}; 
    int[] input3 = {1, 4, 6, 8}; 
    ArrayExamples.reverseInPlace(input1);
    ArrayExamples.reverseInPlace(input2);
    ArrayExamples.reverseInPlace(input3);
    assertArrayEquals(new int[]{ 3 }, input1);
    assertArrayEquals(new int[] {9, 7, 5}, input2);
    assertArrayEquals(new int[] {8, 6, 4, 1}, input3);
  }


  @Test
  public void testReversed() {
    int[] input1 = { }; // NOT failure-inducing input
    int[] input2 = {0, 1, 2};
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
    assertArrayEquals(new int[]{2, 1, 0}, ArrayExamples.reversed(input2));
  }
  
  @Test
  public void testAverageWithoutLowest() {
    double[] input1 = {1.0, 2.0, 3.0}; // NOT failure-inducing input
    double[] input2 = {1.0, 1.0, 2.0, 3.0};
    assertEquals(2.5, ArrayExamples.averageWithoutLowest(input1), 0.0001);
    assertEquals(2.5, ArrayExamples.averageWithoutLowest(input2), 0.0001);
  }
    
}
```
I will list the inputs here as well. For the testReverseInPlace() function, the input, [3], does not cause an error. In testReversed(), the input, [], does not cause any errors. In testAverageWithoutLowest(), the input, [1.0, 2.0, 3.0], does not produce any errors.

## Symptoms
![symptoms](https://i.imgur.com/hsL66VJ.png)
In this screenshot, it is showing the symptoms for the following input. For testReverseInPlace(), it is showing the symptom of the failure-inducing input, [5, 7, 9]. For testReverse(), it is showing the symptom of the failure-inducing input, [0, 1, 2]. For testAverageWithoutLowest(), it is showing the symptom of the failure-inducing input, [1.0, 1.0, 2.0, 3.0].

## Bug Fixes
Below shows the original code, before anything was fixed.
```
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }


}
```

Below is the code after the bug fixes, with the changes labelled with a comment.
```
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {  //added change
      int temp = arr[i];                // added change
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;   // added change
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];  // added change
    }
    return newArray;  // added changes
  }

  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    int numCount = 0;  // added change
    for(double num: arr) {
      if(num != lowest) { 
        sum += num;
        numCount++;  // added change
      }
    }
    return sum / numCount;  /added change
  }

}
```
For reverseInPlace, the bug was that it never saved the element that it was replacing, so it ends up just replacing the first half of the values with the last half of the values in the array. To fix this, I created a variable, temp, to store the replaced value and then sets the corresponding array value to temp. To prevent from swapping back, I changed the for-loop to terminate when i < arr.length/2, when i reaches halfway through the array.

For reversed, the bug was that it sets arr[i] to newArray[arr.length - i - 1], but newArray hasn't been instantiated yet, so it's just filled with 0. Therefore the bug was that it set all the values in arr[] to 0. To fix this bug, I simply swapped the assignment to newArray[i] = arr[arr.length - i - 1] and then returned the newArray.

For averageWithoutLowest, the bug was that if there was multiple occurrences of the lowest element, it does not take that into account when returning the average. To fix this bug, I created a variable to keep count of the number of elements added to sum, and then to get the average, divided the sum by numCount.

# Part 2 - Researching Commands

## Command options for find
All options below were found through the [Linux manual page](https://man7.org/linux/man-pages/man1/find.1.html)
1. -type x
2. -empty
3. -depth
4. -delete

## Examples for each option
### -type x

Example 1
```
jussttin@justins-air docsearch % find ./technical -type d
./technical
./technical/government
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Gen_Account_Office
./technical/government/Post_Rate_Comm
./technical/government/Media
./technical/plos
./technical/biomed
./technical/911report
```
The -type option finds all the files/directories that have the type, x, where x represents the value of the type. In this example, the value is 'd' which is telling the console to find all the directories, within ./technical. This is important because when using ls to list the contents of a directory, there's no way of telling which ones are files and which ones are directories. 

Example 2
```
jussttin@justins-air docsearch % find ./technical/911report/chapter-1.txt -type f
./technical/911report/chapter-1.txt
jussttin@justins-air docsearch % find ./technical/911report/chapter-1.txt -type d
jussttin@justins-air docsearch % 
```
For this example, I used the value 'f' as well, which tells the console to find and list all of the files that are stored in the specified file or directory. In this example, I used the command on a file within ./technical. When running it with the "-type f" option, it printed out the file name, but did not print anything when run with "-type d". This is because the parameter was a file and not a directory. This is useful if you want to quickly check what type of content it is.
### -empty

Example 1
```
jussttin@justins-air docsearch % find ./technical -empty
jussttin@justins-air docsearch % 
```
The option, -empty, lists all empty files. Since there are no empty files in ./technical, it doesn't print anything. This would be useful because it could let the user know whether there are contents in certain files or not. If the user wanted to write into a file without overwriting any data, the user could use -empty to find any empty files that they could use.

Exmaple 2
```
jussttin@justins-air docsearch % find ./technical/911report/chapter-1.txt -empty
jussttin@justins-air docsearch % 
```
For this example, I tried using the option on a file. Since the specific file was filled with text, it's not considered as empty, so the console does not print the file name to the terminal. This is useful for when users need to quickly check whether a specific file has any content in it, for some purposes.
### -depth

Example 1
```
jussttin@justins-air docsearch % find ./technical/government -depth
./technical/government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt
./technical/government/About_LSC/Progress_report.txt
./technical/government/About_LSC/Strategic_report.txt
./technical/government/About_LSC/Comments_on_semiannual.txt
./technical/government/About_LSC/Special_report_to_congress.txt
./technical/government/About_LSC/CONFIG_STANDARDS.txt
./technical/government/About_LSC/commission_report.txt
./technical/government/About_LSC/LegalServCorp_v_VelazquezDissent.txt
./technical/government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt
./technical/government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt
./technical/government/About_LSC/diversity_priorities.txt
./technical/government/About_LSC/reporting_system.txt
./technical/government/About_LSC/State_Planning_Report.txt
./technical/government/About_LSC/Protocol_Regarding_Access.txt
./technical/government/About_LSC/ODonnell_et_al_v_LSCdecision.txt
./technical/government/About_LSC/conference_highlights.txt
./technical/government/About_LSC/State_Planning_Special_Report.txt
./technical/government/About_LSC
./technical/government/emptyCode.java
./technical/government/Env_Prot_Agen/multi102902.txt
./technical/government/Env_Prot_Agen/section-by-section_summary.txt
./technical/government/Env_Prot_Agen/jeffordslieberm.txt
./technical/government/Env_Prot_Agen/final.txt
./technical/government/Env_Prot_Agen/ctf7-10.txt
./technical/government/Env_Prot_Agen/ctf1-6.txt
./technical/government/Env_Prot_Agen/ro_clear_skies_book.txt
./technical/government/Env_Prot_Agen/ctm4-10.txt
./technical/government/Env_Prot_Agen/1-3_meth_901.txt
./technical/government/Env_Prot_Agen/atx1-6.txt
./technical/government/Env_Prot_Agen/tech_sectiong.txt
./technical/government/Env_Prot_Agen/bill.txt
./technical/government/Env_Prot_Agen/nov1.txt
./technical/government/Env_Prot_Agen/tech_adden.txt
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems/Session2-PDF.txt
./technical/government/Alcohol_Problems/Session3-PDF.txt
./technical/government/Alcohol_Problems/DraftRecom-PDF.txt
./technical/government/Alcohol_Problems/Session4-PDF.txt
./technical/government/Alcohol_Problems
./technical/government/Gen_Account_Office/d0269g.txt
./technical/government/Gen_Account_Office/Testimony_cg00010t.txt
./technical/government/Gen_Account_Office/og97032.txt
./technical/government/Gen_Account_Office/og99036.txt
./technical/government/Gen_Account_Office/GovernmentAuditingStandards_yb2002ed.txt
./technical/government/Gen_Account_Office/Sept27-2002_d02966.txt
./technical/government/Gen_Account_Office/d01376g.txt
./technical/government/Gen_Account_Office/Statements_Feb28-1997_volume.txt
./technical/government/Gen_Account_Office/og97019.txt
./technical/government/Gen_Account_Office/pe1019.txt
./technical/government/Gen_Account_Office/Testimony_Jul15-2002_d02940t.txt
./technical/government/Gen_Account_Office/gg96118.txt
./technical/government/Gen_Account_Office/og97020.txt
./technical/government/Gen_Account_Office/ffm.txt
./technical/government/Gen_Account_Office/og97023.txt
./technical/government/Gen_Account_Office/July11-2001_gg00172r.txt
./technical/government/Gen_Account_Office/d01121g.txt
./technical/government/Gen_Account_Office/og96011.txt
./technical/government/Gen_Account_Office/d03419sp.txt
./technical/government/Gen_Account_Office/Letter_Walkeraug17let.txt
./technical/government/Gen_Account_Office/og97051.txt
./technical/government/Gen_Account_Office/og97045.txt
./technical/government/Gen_Account_Office/Testimony_d01609t.txt
./technical/government/Gen_Account_Office/og97050.txt
./technical/government/Gen_Account_Office/og96038.txt
./technical/government/Gen_Account_Office/og98029.txt
./technical/government/Gen_Account_Office/Sept14-2002_d011070.txt
./technical/government/Gen_Account_Office/d03273g.txt
./technical/government/Gen_Account_Office/Oct15-1999_gg00026t.txt
./technical/government/Gen_Account_Office/og96012.txt
./technical/government/Gen_Account_Office/og97046.txt
./technical/government/Gen_Account_Office/og97052.txt
./technical/government/Gen_Account_Office/d03232sp.txt
./technical/government/Gen_Account_Office/og97043.txt
./technical/government/Gen_Account_Office/June30-2000_gg00135r.txt
./technical/government/Gen_Account_Office/d01591sp.txt
./technical/government/Gen_Account_Office/Oct15-2001_d0224.txt
./technical/government/Gen_Account_Office/og96028.txt
./technical/government/Gen_Account_Office/og96014.txt
./technical/government/Gen_Account_Office/og97041.txt
./technical/government/Gen_Account_Office/og96015.txt
./technical/government/Gen_Account_Office/d01145g.txt
./technical/government/Gen_Account_Office/InternalControl_ai00021p.txt
./technical/government/Gen_Account_Office/og96031.txt
./technical/government/Gen_Account_Office/d01186g.txt
./technical/government/Gen_Account_Office/og96033.txt
./technical/government/Gen_Account_Office/og96027.txt
./technical/government/Gen_Account_Office/og98022.txt
./technical/government/Gen_Account_Office/og96026.txt
./technical/government/Gen_Account_Office/og96032.txt
./technical/government/Gen_Account_Office/im814.txt
./technical/government/Gen_Account_Office/og96036.txt
./technical/government/Gen_Account_Office/og96022.txt
./technical/government/Gen_Account_Office/og96023.txt
./technical/government/Gen_Account_Office/og96037.txt
./technical/government/Gen_Account_Office/og98032.txt
./technical/government/Gen_Account_Office/og98026.txt
./technical/government/Gen_Account_Office/og98030.txt
./technical/government/Gen_Account_Office/og98024.txt
./technical/government/Gen_Account_Office/og96009.txt
./technical/government/Gen_Account_Office/og96021.txt
./technical/government/Gen_Account_Office/og98018.txt
./technical/government/Gen_Account_Office/ai00134.txt
./technical/government/Gen_Account_Office/og96034.txt
./technical/government/Gen_Account_Office/og98019.txt
./technical/government/Gen_Account_Office/og96020.txt
./technical/government/Gen_Account_Office/Testimony_Jul17-2002_d02957t.txt
./technical/government/Gen_Account_Office/og96047.txt
./technical/government/Gen_Account_Office/ai9868.txt
./technical/government/Gen_Account_Office/og98041.txt
./technical/government/Gen_Account_Office/og97038.txt
./technical/government/Gen_Account_Office/Paper_Walker11-2002_acpro122.txt
./technical/government/Gen_Account_Office/og97011.txt
./technical/government/Gen_Account_Office/og97039.txt
./technical/government/Gen_Account_Office/May1998_ai98068.txt
./technical/government/Gen_Account_Office/og98040.txt
./technical/government/Gen_Account_Office/og96045.txt
./technical/government/Gen_Account_Office/og98044.txt
./technical/government/Gen_Account_Office/og96041.txt
./technical/government/Gen_Account_Office/d02701.txt
./technical/government/Gen_Account_Office/og97001.txt
./technical/government/Gen_Account_Office/og97028.txt
./technical/government/Gen_Account_Office/ai2132.txt
./technical/government/Gen_Account_Office/Letter_WalkerJan30-2001.txt
./technical/government/Gen_Account_Office/og96040.txt
./technical/government/Gen_Account_Office/og98045.txt
./technical/government/Gen_Account_Office/og96042.txt
./technical/government/Gen_Account_Office/og97002.txt
./technical/government/Gen_Account_Office/og97003.txt
./technical/government/Gen_Account_Office/og96043.txt
./technical/government/Gen_Account_Office/og98046.txt
./technical/government/Gen_Account_Office
./technical/government/Post_Rate_Comm/Gleiman_EMASpeech.txt
./technical/government/Post_Rate_Comm/Mitchell_spyros-first-class.txt
./technical/government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt
./technical/government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt
./technical/government/Post_Rate_Comm/Mitchell_RMVancouver.txt
./technical/government/Post_Rate_Comm/Gleiman_gca2000.txt
./technical/government/Post_Rate_Comm/Cohenetal_Cost_Function.txt
./technical/government/Post_Rate_Comm/Redacted_Study.txt
./technical/government/Post_Rate_Comm/Mitchell_6-17-Mit.txt
./technical/government/Post_Rate_Comm/Cohenetal_comparison.txt
./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt
./technical/government/Post_Rate_Comm/Cohenetal_RuralDelivery.txt
./technical/government/Post_Rate_Comm/ReportToCongress2002WEB.txt
./technical/government/Post_Rate_Comm/WolakSpeech_usps.txt
./technical/government/Post_Rate_Comm
./technical/government/Media/Federal_agency.txt
./technical/government/Media/water_fees.txt
./technical/government/Media/Helping_Out.txt
./technical/government/Media/balance_scales_of_justice.txt
./technical/government/Media/BusinessWire2.txt
./technical/government/Media/Legal-aid_chief.txt
./technical/government/Media/Unusual_Woodburn.txt
./technical/government/Media/Funding_cuts_force.txt
./technical/government/Media/Good_guys_reward.txt
./technical/government/Media/Anthem_Payout.txt
./technical/government/Media/Donald_Hilliker.txt
./technical/government/Media/Free_legal_service.txt
./technical/government/Media/Owning_a_Piece.txt
./technical/government/Media/Targeting_Domestic_Violence.txt
./technical/government/Media/highlight_Senior_Day.txt
./technical/government/Media/State_funding.txt
./technical/government/Media/Few_who_need.txt
./technical/government/Media/City_Council_Budget.txt
./technical/government/Media/Legal_system_fails_poor.txt
./technical/government/Media/Supporting_Legal_Center.txt
./technical/government/Media/Lindsays_legacy.txt
./technical/government/Media/New_funding_sources.txt
./technical/government/Media/Barnes_new_job.txt
./technical/government/Media/Providing_Legal_Aid.txt
./technical/government/Media/Nonprofit_Buys.txt
./technical/government/Media/Legal_Aid_in_Clay_County.txt
./technical/government/Media/Domestic_Violence_Ruling.txt
./technical/government/Media/Abuse_penalties.txt
./technical/government/Media/Law_Award_from_College.txt
./technical/government/Media/Law_Schools.txt
./technical/government/Media/Raising_the_Bar.txt
./technical/government/Media/Justice_for_all.txt
./technical/government/Media/agency_expands.txt
./technical/government/Media/Helping_Hands.txt
./technical/government/Media/Legal_hotline.txt
./technical/government/Media/not_accessible_to_disabled.txt
./technical/government/Media/Campaign_Pays.txt
./technical/government/Media/New_Online_Resources.txt
./technical/government/Media/Annual_Fee.txt
./technical/government/Media/Oregon_Poor.txt
./technical/government/Media/Barnes_pro_bono.txt
./technical/government/Media/Poor_Lacking_Legal_Aid.txt
./technical/government/Media/Paralegal_Honored.txt
./technical/government/Media/Workers_aid_center.txt
./technical/government/Media/Philly_Lawyers.txt
./technical/government/Media/Too_Crucial_to_Take_Cut.txt
./technical/government/Media/Pro_Bono_Services.txt
./technical/government/Media/Rumble_in_the_Bronx.txt
./technical/government/Media/FortWorthStarTelegram.txt
./technical/government/Media/predatory_loans.txt
./technical/government/Media/Survey.txt
./technical/government/Media/AP_LawSchoolDebts.txt
./technical/government/Media/Working_for_Free.txt
./technical/government/Media/Eviction_law.txt
./technical/government/Media/Law-school_grads.txt
./technical/government/Media/FY_04_Budget_Outlook.txt
./technical/government/Media/help_rent-to-own_tenants.txt
./technical/government/Media/Texas_Lawyer.txt
./technical/government/Media/Disaster_center.txt
./technical/government/Media/Kiosks_for_court_forms.txt
./technical/government/Media/Higher_Registration_Fees.txt
./technical/government/Media/Fire_Victims_Sue.txt
./technical/government/Media/Funds_Shortage.txt
./technical/government/Media/Terrorist_Attack.txt
./technical/government/Media/Butler_Co_attorneys.txt
./technical/government/Media/BergenCountyRecord.txt
./technical/government/Media/families_saved.txt
./technical/government/Media/Court_Keeps_Judge_From.txt
./technical/government/Media/Volunteers_Step_Up.txt
./technical/government/Media/Coup_Reshapes_Legal_Aid.txt
./technical/government/Media/IOLTA_INTEREST_RATE.txt
./technical/government/Media/Ginny_Kilgore.txt
./technical/government/Media/Legal_Aid_looks_to_legislators.txt
./technical/government/Media/Poverty_Lawyers.txt
./technical/government/Media/Wingates_winds.txt
./technical/government/Media/Avoids_Budget_Cut.txt
./technical/government/Media/grants_fail_to_come.txt
./technical/government/Media/Lockyer_Warns.txt
./technical/government/Media/It_Pays_to_Know.txt
./technical/government/Media/Self-Help_Website.txt
./technical/government/Media/Rental_rules.txt
./technical/government/Media/Using_Tech_Tools.txt
./technical/government/Media/Assuring_Underprivileged.txt
./technical/government/Media/Boone_legal_service.txt
./technical/government/Media/Firm_to_the_Poor_Needs_Help.txt
./technical/government/Media/Making_a_case.txt
./technical/government/Media/Barnes_Volunteers.txt
./technical/government/Media/Commercial_Appeal.txt
./technical/government/Media/Justice_requests.txt
./technical/government/Media/Free_Legal_Assistance.txt
./technical/government/Media/Local_Attorneys.txt
./technical/government/Media/Texas_Supreme_Court.txt
./technical/government/Media/Civil_Matters.txt
./technical/government/Media/Low-income_children.txt
./technical/government/Media/man_on_national_team.txt
./technical/government/Media/BusinessWire.txt
./technical/government/Media/Funding_May_Limit.txt
./technical/government/Media/The_Columbian.txt
./technical/government/Media/Higher_court.txt
./technical/government/Media/Service_Agency.txt
./technical/government/Media/Marylands_Legal_Aid.txt
./technical/government/Media/Bias_on_the_Job.txt
./technical/government/Media/Attorney_gives_his_time.txt
./technical/government/Media/Library_Lawyers.txt
./technical/government/Media/Crains_New_York_Business.txt
./technical/government/Media/Hard_to_Get.txt
./technical/government/Media/The_State_of_Pro_Bono.txt
./technical/government/Media/residents_sue_city.txt
./technical/government/Media/Legal_Aid_Society.txt
./technical/government/Media/GreensburgDailyNews.txt
./technical/government/Media/Major_Changes.txt
./technical/government/Media/Program_Lodges.txt
./technical/government/Media/Wilmington_lawyer.txt
./technical/government/Media/All_May_Have_Justice.txt
./technical/government/Media/Domestic_violence_aid.txt
./technical/government/Media/Advocate_for_Poor.txt
./technical/government/Media/fight_domestic_abuse.txt
./technical/government/Media/CommercialAppealMemphis2.txt
./technical/government/Media/Weak_economy.txt
./technical/government/Media/Lawyer_Web_Survey.txt
./technical/government/Media/Valley_Needing_Legal_Services.txt
./technical/government/Media/Barr_sharpening_ax.txt
./technical/government/Media/Legal_Aid_attorney.txt
./technical/government/Media/The_Bend_Bulletin.txt
./technical/government/Media/Legal_services_for_poor.txt
./technical/government/Media/Farm_workers.txt
./technical/government/Media/Entities_Merge.txt
./technical/government/Media/less_legal_aid.txt
./technical/government/Media/Understanding.txt
./technical/government/Media/Do-it-yourself_divorce.txt
./technical/government/Media/Politician_Practices.txt
./technical/government/Media/defend_yourself.txt
./technical/government/Media/Towson_Attorney.txt
./technical/government/Media/Pro-bono_road_show.txt
./technical/government/Media/A_Perk_of_Age.txt
./technical/government/Media/A_helping_hand.txt
./technical/government/Media/pro_bono_efforts.txt
./technical/government/Media/5_Legal_Groups.txt
./technical/government/Media/Greedy_Generous.txt
./technical/government/Media/Retirement_Has_Its_Appeal.txt
./technical/government/Media/RoanokeTimes.txt
./technical/government/Media/NJ_Legal_Services.txt
./technical/government/Media/Bridging_legal_aid_gap.txt
./technical/government/Media/Legal_Aid_campaign.txt
./technical/government/Media/Aid_Gets_7_Million.txt
./technical/government/Media
./technical/government
```
For a directory, the option, "-depth", recursively runs through all files and directories and lists all the respective paths within the directory. This is useful because it allows you to easily see the structure of the workspace, especially when working from a remote computer, where you can't see the file structure on your own computer. The option causes the console to list all files within a directory, followed by the path for that directory.

Example 2
```
jussttin@justins-air docsearch % find ./technical/911report/preface.txt -depth
./technical/911report/preface.txt
jussttin@justins-air docsearch % 
```
For a file, this option just simply prints out the path of the file. This is useful if you simply just want the relative path to a certain file.

### -delete

Example 1
```
jussttin@justins-air docsearch % find ./technical/plos -delete
jussttin@justins-air docsearch % 
```
Although there isn't much to show in the terminal, if you look at the workspace, shown in the screenshot below, the directory, plos, was deleted, along with all the files within it. <br>
![workspace](https://i.imgur.com/AqVhzm3.png) <br>
This is useful if you ever want to delete a whole batch of files. You don't have delete each file one by one. This is especially useful for directories that contain a huge amount of files.

Exampel 2
```
jussttin@justins-air docsearch % find ./technical/911report/chapter-1.txt -delete
jussttin@justins-air docsearch % 
```
When used on a file, there is a similar effect. As shown below, the file is now gone, deleted. <br>
![workspace](https://i.imgur.com/TVziTDS.png) <br>
This is useful if you know the relative or absolute path of a file. If the file is embedded in a whole bunch of directories, it might take a while to find the file and delete it manually. But if you know the relative or absolute path of the file, you can use the "-delete" function to easily delete the file without having to manually find it.
