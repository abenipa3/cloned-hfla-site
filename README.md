# Cloned HFLA Site Test

Hack for LA's Website Team plans to build a replica of their live website that would encourage more of their teammates to review pull requests regardless of their experience in development (specifically GitHub). The replica will be used to perform updates safely before implementing changes to the live website as well as upload and delete forked repos.

For testing purposes, I will be using Netlify to deploy this cloned repo and document my findings.

More details can also be found in the following issues:
- [Research How to Host a Replica of Our Website](https://github.com/hackforla/website/issues/2014)

# Findings for Each Interfaces Researched

<details> <summary> squash.io </summary>

- Steps I took to Test and Research:
   - Created an account.
   - Selected “New Deployment.”
- Testing:
   - Tested the hfla/website forked to my repo and this is the result.
![image](https://user-images.githubusercontent.com/38295612/129712832-83b572cf-c586-4b6e-a327-5ba2bf122c25.png)
   - Decided to test with a clone of the Guide Pages Prototype.
- Results:
   - squash.io provides a time limit in how long the deployment will run before it expires.
   - Test did not succeed as seen in the logs below.

![image](https://user-images.githubusercontent.com/38295612/129712957-d60b57d6-ed70-40d0-9cba-917f14e919e1.png)

![image](https://user-images.githubusercontent.com/38295612/129712988-5ba17873-8526-446c-9662-7560d8f495eb.png)

- FYI:
   - The free version of this website allows 30 hours/month of deployment.
       - Once the 30 hours expire, it will take a month to reset.

</details> 

<details> <summary> travis-ci </summary>

- Steps I took to Test and Research:
    - Created an account.
    - Added a `.travis.yml` file to my prototype's repository to tell Travis CI what to do.
- Testing:
  - Tested the hfla/website forked to my repo and a couple of prototypes. All resulted in this:
![image](https://user-images.githubusercontent.com/38295612/129713418-07959668-61e0-42cb-b556-0647c9728a68.png)
  - I added a .travis.yml file to my prototypes (excluding the hfla/website as I was cautious about doing so even though it's in my repo), and pushed to my github repo. 
  - Results:
     - No progress. 
     - Researched why it was the case and found these links from the Travis-CI community [here](https://travis-ci.community/t/no-builds-for-this-repository-and-no-requests-for-a-travis-ci-org-organization-repo/11443) and [here](https://travis-ci.community/t/no-builds-for-this-repository/151/3) as well as the [Jekyll’s Docs on Travis-CI](https://jekyllrb.com/docs/continuous-integration/travis-ci/). 
     - Still didn’t get the help needed, so I moved on to the next option (netlify).

</details> 

<details> <summary> netlify </summary>

- Must have a netlify account.
- Select “New Site from Git”
- Under Continuous Deployment, select the repository you want to deploy.
- Testing:
   - Tested with a clone of the Guide Pages Prototype.
   - Setting up was straightforward. Must have a Gemfile to have a working build. Was able to migrate jekyll site to netlify with this [link](https://www.netlify.com/blog/2017/05/11/migrating-your-jekyll-site-to-netlify/).
- Results:
   - Total deploy time: 20s.
   - Succeeded in deploying the cloned website [here](https://pages-clone-test.netlify.app/).
   - _One does not simply deploy a cloned website without encountering bugs, however..._
   - Stylings were missing as seen below. 
![image](https://user-images.githubusercontent.com/38295612/129714705-6663511d-ec7b-48ac-a516-340a5e00c820.png)
   - The links to the cloned guide pages lead to an error page. 
![image](https://user-images.githubusercontent.com/38295612/129714792-05eaf8f6-e2f3-4114-bfe3-1e6f8c1b7213.png)
   - To navigate to the working links of the individual guide pages, must delete  /pages-clone-test/ in https://pages-clone-test.netlify.app/pages-clone-test/github-issues. Example: https://pages-clone-test.netlify.app/github-issues
   - Is it feasible?
       - So far, no. Unless we find out how to deploy a clone without the errors mentioned above.
       - However, I would like to know our team's thoughts on this to see we could work through the errors.


</details> 

# Deploying HfLA Live Website to Netlify

## Prerequisites
Note: Most of the links mentioned in this section contain visuals of the steps taken to fulfill this process.

- Create an account for Hack for LA by using GitHub or Email.
- Select ["New Site"](https://user-images.githubusercontent.com/38295612/132080562-7f51bcd0-f0d1-4485-a07b-86e80b1f2245.png) from Git. 
- The site will take you to the “Create a new site” page. Under [Continuous Deployment](https://user-images.githubusercontent.com/38295612/132077771-d0a05dd1-6f86-4bba-8bc3-754a84587a3a.png), select GitHub.


- Follow the instructions. Select the repository you want to link to your site on Netlify. 
   - If you can’t see your repo, [configure the Netlify app on GitHub](https://github.com/apps/netlify/installations/new).

- A message in a [yellow box](https://user-images.githubusercontent.com/38295612/132077797-f690335d-776c-4895-8554-27f3019107c0.png) will appear on the screen. 
    - In this case, we will need to add a **Gemfile** before we can proceed. 
    - It will contain two lines in the file as seen [here](https://user-images.githubusercontent.com/38295612/132078081-75a48466-6efa-4b0d-a563-fb366a08019c.png).

- When completed, select Deploy Site. Wait for the site to build. Duration takes approx. 7 seconds. 
    - A [message ](https://user-images.githubusercontent.com/38295612/132077858-682cc38e-df1e-412d-a0fa-51d8f667a98c.png)will indicate when the site has been successfully deployed.


## Limitations

- [Bandwidth Used](https://docs.netlify.com/accounts-and-billing/billing/#bandwidth-usage) 
   - Bandwidth counter increases when the number of users visit the site. [[Source]](https://answers.netlify.com/t/what-does-actually-count-in-bandwidth/28605/4)
      - If one user spams the website with visits, the counter would increase as Netlify serves content to that user.
   - Every CSS, JS file served by the website would count against the bandwidth quota.
- [Build Minutes Used](https://docs.netlify.com/accounts-and-billing/billing/#builds-usage)
    - Time spent uploading new or changed files resulting from the build does count in the build minutes. [[Source]](https://answers.netlify.com/t/what-does-consitute-build-time/3889/8)
    - The time spent deploying after building does not count. [[Source]](https://answers.netlify.com/t/what-does-consitute-build-time/3889/3)
    - To check builds status and manage build capacity, visit `https://app.netlify.com/teams/[netlify account name]/builds/`
- Concurrent Builds
    - If we plan to build more than one website, there is no additional charge beyond the plan price for any plan - Starter, Pro, or Business - to queue up builds beyond the concurrency limit. [[Source]](https://answers.netlify.com/t/how-do-concurrent-builds-work/20086/2)
- Members
  - Must [pay](https://user-images.githubusercontent.com/38295612/132078598-594d697f-32f4-4504-b0b7-65a466fca2e2.png) to add more than one member. 
  - In this case, we'll have one team member maintaining the netlify account to keep to the free plan.

## Our Goals with Netlify
- Encourage more team members to review pull requests using the cloned website.
- Use Netlify's free plan for our weekly demos (specifically our Sunday Team meetings) before merging changes.

## Additional Resources
- [How to configure the Netlify app on GitHub?](https://github.com/apps/netlify/installations/new) - How to add repo to Netlify.
- [Netlify Billing](https://docs.netlify.com/accounts-and-billing/billing/) - More details on Builds Usage, Bandwidth Usage, etc.
- [Pricing Plan](https://www.netlify.com/pricing/) - Added this as reference to what's included in the free plan.
- [Build Minutes Pricing FAQ](https://www.netlify.com/pricing/faq/) - More details on Build Minutes.


# Cloned Website
https://cloned-hfla-site.netlify.app/

# Live Website

Hack for LA's website: https://www.hackforla.org
