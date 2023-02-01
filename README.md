# Sailpoint
Here is my presentation task of SailPoint training.
6.Write a rule to return attribute distinguishedName(dn) of specific identity from AD application.
  
  List userName = new ArrayList();
  QueryOptions qo = new QueryOptions();
  qo.addFilter(Filter.eq("links.application.name", "AD Application"));
  List users = context.getObjects(Identity.class);
  for(Identity iden:users){
    user = "CN="+identity.getFullName()+",OU=Persons,DC=SP,DC=LOCAL";
    userName.add("DistinguishedName : " + user);
  }
  return userName;

  Identity identity = context.getObjectByName(Identity.class,"XKBP");
  return "CN="+identity.getFullName()+",OU=Persons,DC=SP,DC=LOCAL";


7.Write a rule to return the attribute samAccountName of a specific identity from the AD application.

  List userName = new ArrayList();
  QueryOptions qo = new QueryOptions();
  qo.addFilter(Filter.eq("links.application.name", "AD Application"));
  List users = context.getObjects(Identity.class);
  for(Identity iden:users)
  {
    userName.add("samAccountName : " + iden.getName());
  }
  return userName;


8.Write a rule to get the list of users who has Active Directory applications.
 
  Use QueryOptions and Filter.Hint Filter.eq(“links.application.name”, “Active Directory”);

  List userName = new ArrayList();
  QueryOptions qo = new QueryOptions();
  qo.addFilter(Filter.eq("links.application.name", "AD Application"));
  List users = context.getObjects(Identity.class, qo);
  for(Identity iden:users)
  {
    userName.add("Employee under RBVH manager : " + iden.getName());
  }
 return userName;

9.Write a rule to return lists of identity with a specific manager. User query options and filter. Hint Filter.eq(“”manager.name”, “RBVH”).

  List userName = new ArrayList();
  
  QueryOptions qo = new QueryOptions();
  qo.addFilter(Filter.eq("manager.name", "RBVH"));
  List users = context.getObjects(Identity.class, qo);
  for(Identity iden:users)
  {
    userName.add("Employee under RBVH manager : " + iden.getName());
  }
 return userName;

10.Write a rule to return entitlements from particular  Applications.
 List list = new ArrayList();
  List managedattributelist = context.getObjects(ManagedAttribute.class);
  for(ManagedAttribute Entitlements:managedattributelist){
     if (Entitlements.getApplication().getName().equals("AD Application")){
      list.add(Entitlements.getValue());
    }
  }
  return list;


11.Write a rule to return  particular identityAttribute(departmentName, email) for user.
 ArrayList list = new ArrayList();
 Identity identity = context.getObjectByName(Identity.class, "RBVH");

 Object DeptNum = identity.getAttribute("Department Number");
 Object email = identity.getAttribute("email");
 list.add (DeptNum);
 list.add(email);
 return list;


Identity identity = context.getObjectByName(Identity.class,"XKBP");
Object status = identity.getStringAttribute("Status");
Object email = identity.getAttribute("email");
return status + "," + email;

12.Write a rule to return all the certifications in your system and its certifiers.
  List allcertifiers = new ArrayList();
  List certList = context.getObjects(Certification.class);
  if(cert != null ){
    for(Certification cert: certList){
      List cerifiers = cert.getCertifiers();
        String cer = cert.getName();
      if(cerifiers != null){
        allCertifiers.addAll(cerifiers); 
        allCertifiers.add(cer);
      }
    }
  }

 return new HashSet(allCertifiers);

13.Write a rule to return all the roles and their corresponding owner.
 List roleList = new ArrayList();
  List role = context.getObjects(Bundle.class);
  Identity roleOwn = context.getObjectByName(Identity.class, approver);
  for (Bundle rol:role){
    if(rol != null){
      List rols = roleOwn.getName();
        String rolName = rol.getName();
      if(rols != null){
        roleList.add(rols);
        roleList.add(rolName);
    }
    }
  }
  return roleList;

14.Write a rule to return one business role and its IT roles.
  List roleList = new ArrayList();
  List role = context.getObjects(Bundle.class);
  for (Bundle rol:role){
    //return rol;
    if(rol.getType().equals("business")){
      String rols = rol.getName();
        List rolName = rol.getRole();
      //if(rols != null){
        roleList.add(rols);
        roleList.add(rolName);
    }
    }
  }
  return roleList;


15.Write a rule to return all workflows with the “ LCMProvisioning “ type.
  List workList = new ArrayList();
  QueryOptions qo = new QueryOptions();
  qo.addFilter(Filter.eq("type", "LCMProvisioning"));
  List workflow = context.getObjects(Workflow.class,qo);
  for(Workflow wflow:workflow){
    if(wflow != null){
      String flow = wflow.getName();
      workList.add(flow);
    }
  }
  return workList;

16.Write a rule to create a new custom object and populate the custom object with the key as a user and the value as email.
  Custom customObject = new Custom();
  customObject.setName("CUSTOM_USER_DETAILS");
  customObject.put("user", "email");

  context.saveObject(customObject);
  context.commitTransaction();
  return "Done";

  Custom customObject = new Custom();
  customObject.setName("CUSTOM_USER_DETAILS");
  customObject.put("user", "email");

  context.saveObject(customObject);
  context.commitTransaction();

17.Write a rule to find a list of users who have particular managers, who have AD applications, and whose email is not null. Use QueryOptions and filter.
#Identity,Application

  List userNames = new ArrayList();
  QueryOptions qo = new QueryOptions();
  qo.addFilter(Filter.eq("manager.name", "RBVH"));
  qo.addFilter(Filter.eq("links.application.name", "AD Application"));
  qo.addFilter(Filter.ne("email", ""));
  List users = context.getObjects(Identity.class, qo);
  if(users != null){
    for(Identity iden:users){
      userNames.add(iden.getName());
    } 
  }
  return userNames;

18.Write a rule to return all requestable entitlement in IIQ.
#ManagedAttribute
  List list = new ArrayList();
  QueryOptions qo = new QueryOptions();
  qo.addFilter(Filter.eq("requestable", true));
  List managed = context.getObjects(ManagedAttribute.class,qo);
  for (ManagedAttribute entit:managed){
    String mask = entit.getDisplayName();
    list.add(mask);
  }
  return list;

19.Write a rule to return the description and owner of entitlements in IIQ.
  List desowner = new ArrayList();
  List entitlement = context.getObjects(ManagedAttribute.class);
  for(ManagedAttribute ent:entitlement){
    if(ent != null){
      description = ent.getDescription();
      owner = ent.getOwner();
      desowner.add(description);
      desowner.add(owner);
  }
  }
  return desowner;


20.Write a rule to return the list of application/account identity has.

  List list = new ArrayList();
  List ident = context.getObjects(ManagedAttribute.class);
  if(ident != null){
    for(ManagedAttribute account:ident){
      app = account.getApplication();
      list.add(app);
  }
  }
  return list;
  
22.Write a rule to return all active directory entitlements in IIQ.
  
  List appName = new ArrayList();
  
  QueryOptions qo = new QueryOptions();
  qo.addFilter(Filter.eq("application.name", "AD Application"));
  
  List name = context.getObjects(ManagedAttribute.class,qo);
  if(name !=null){
    for(ManagedAttribute ent:name){
      naam = ent.getValue();
      appName.add(naam);
  }
  }
  return appName;

23.Write a rule to return all users from an authoritative source in IIQ.
  List appName = new ArrayList();
  
  QueryOptions qo = new QueryOptions();
  qo.addFilter(Filter.eq("links.application.authoritative", true));
  
  List name = context.getObjects(Identity.class,qo);
  //List boos = context.getObjects(Identity.class,qo);
  if(name !=null){
    for(Identity ent:name){
      naam = ent.getDisplayName();
      appName.add(naam);
  }
  }
  return appName;

24.Write a rule to return all the identities that are managers.

  List list = new ArrayList();
  List boos = context.getObjects(Identity.class);
  if(boos != null){
    for(Identity mange: boos){
      if(mange.getManagerStatus()){
        String namm = mange.getDisplayName();
        list.add(namm);
          
     }
    }
  }
  return list;

1.Write a rule to determine the Identity's assigned and detected roles.

Identity identity = context.getObjectByName(Identity.class,"XKBP");
  return identity.getDetectedRoles();
  return identity.getAssignedRoles();


2.Write a rule to get the list of active users in SailPoint.

  Map map = new HashMap();
  map.put("firstname","Barack");
  map.put("lastname","Obama");
  map.put("status","Active");
  
  String stattype = map.get("status"); 

  if (stattype.equals("Active")){
   log.error("Employee is Active");
    return "Employee is Active";
  }else{
    return inactive;
  }

3.Write a rule to find all active users in SailPoint and print the user as Lastname.firstname in the console.
  List list = new ArrayList();
  List user = context.getObjects(Identity.class);
  for(Identity active:user){
    if(active != null){
      String lname = active.getLastname();
      fname = active.getFirstname();
      list.add(lname +"."+ fname);
    }
  }
  return list;

4.Write a rule to return a map of users and roles. The returned map should have a key as a user and a value as a list of assigned roles.

Map returnMap = new HashMap();
map.put("Username","Display name");
map.put("Role","role");

String uName = account.getStringAttribute("userName");
String roles = account.getStringAttribute("Roles");
log.error("empID" + empID);

if (uName.equals("X907")) {
  returnMap.put("identityName", roles);
}
return returnMap;
return object;

List list = new ArrayList();
  Map map = new HashMap();
  List uname = context.getObjects(Identity.class);
  if(uname != null){
    List rol = uname.getAssignedRoles();
    map.put("user", "rol");
    String addddd = map.get("user");
    if (rol != null){
      list.add(rol);
    }
  }
  return list;
  
5.Write a rule to get all users’ User Rights(capability). Return in map format with key as user and value as a list of user rights.

Map returnMap = new HashMap();
map.put("Username","Display name");
map.put("Role","role");

String uName = account.getStringAttribute("userName");
String rights = account.getStringAttribute("rights");

if (uName != null) {
  returnMap.put("identityName", rights);
}
return returnMap;
return object;















