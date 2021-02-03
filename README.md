# How to migrate Netflix profiles (export and import ratings, "My-List" and watch history)

Since Netflix didn't provide native APIs to retrieve your profile info, there's no official ways to export your ratings or watch-list and import to the new profile.  

But by doing some tweaks, there's some way to manually export and import the lists for having about 70% completeness.

## Requirement

- Chromium Web Browser (e.g.: [Brave](https://brave.com/))
- [nodejs](https://nodejs.org/en/)

## Steps

### 1. Backup all of your information

1. Open any web browser and install the extension [Netflix List Exporter](https://github.com/daltonmenezes/netflix-list-exporter) written by Dalton Menezes.
2. Login into the old profile and go to your [My-List page](https://www.netflix.com/browse/my-list), there should be 3 buttons to export your upvotes, downvotes and your watch list.
3. save them as text files or `.csv`, will use them as an answer to examine the export/import result.

### 2. Export and Import the ratings

1. We are using the repo from [LBBO's "netflix migrate"](https://github.com/LBBO/netflix-migrate). First, install [nodejs](https://nodejs.org). After the installation complete, open a cli (`bash` if you're running a UNIX/Linux/MacOS or `cmd.exe` if you're running a Windows) and type the below command to install the script:  
`npm install -g netflix-migrate`

2. After installed the script, use the following command to export the ratings from the old profile:  
`netflix-migrate --email old@example.com --profile OldProfileName --export ratings.json`
3. You'll be prompted to enter your Netflix password, if the password and the profile name is correct, a `.json` file will be created under the current directory.
4. Use the following command to import the `.json` ratings to the new profile:  
`netflix-migrate --email new@example.com --profile NewProfileName --import ratings.json`
5. Login into the new profile, or use the text-file/`.csv` you saved in the first step to check if the import is correct and complete. This should be fine. If not, head to the [original repo site](https://github.com/LBBO/netflix-migrate) to find out further support.

### 3. Export and Import Watch List

1. Use the Chromium browser and install this extension: ["Netflix Watch List Manager"](https://chrome.google.com/webstore/detail/netflix-watch-list-manage/obgidigipndchfoaapdbldekffjpmmfa?hl=en).
2. Follow the extension's instruction, first login into the old profile and go to the [MyListOrder page](https://www.netflix.com/mylistorder) and change the list order to munaul instead of Netflix's recommendation.
3. Go to the [My-List page](https://www.netflix.com/browse/my-list) and click the extension icon, and click the "Export" button.
4. This will generate another `.json` file containing your watch list, composed of the title and the movieID. In my case howere, comparing to the text-file/.csv you saved in the first step, there are lacking some of the movies & shows (for me it is 323 out of 351).
5. Next, login into the _new_ profile and go to the [My-List page](https://www.netflix.com/browse/my-list), click the extension icon, and finally click the "Import" button.
6. This should import _all_ of the movies/shows you just export, yet again, I'm encountering some lacking, only got 234 out of 323.
7. If you want to compare what didn't being imported, just export again and compare the two `.json` files, and you can manually add them if you want.

### 4. Import watch history

According to [LBBO's "netflix migrate" repo](https://github.com/LBBO/netflix-migrate), at the time (Feb, 2021) the import function is not fulfill yet.   
Yet, the exported `.json` file (from step 2) do contains all of your viewing history. So once the import function complete you'd be able to import the old viewing history even without the old account/profile as long as you keep the `.json` file .

## Conclusion

This method isn't rock solid, but it do save a lot of time, the more movies/shows you've saved the more time you're going to save.  
With about 70% completeness, you can examine the rest to decide whether to add them munaually or be satisfied for the current position.

## Disclaimer

All of the scripts are googled, and should be use at your own risks.  

As in [LBBO's "netflix migrate" repo](https://github.com/LBBO/netflix-migrate) stated, use of the script may constitute a breach in Netflix's Terms of Use and/or their End User License Agreement. 
