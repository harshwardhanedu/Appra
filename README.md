def get_chrome_version():
  version = None
  try:
    result = subprocess.run(['google-chrome', '--version'], capture_output = True, text = True)
    version = result.stdout.strip().split()[-1]
    return version

  except Exception as e:
    logging.error("Error occurred while fetching Chrome version: %s", e)
    return None
  finally:
    if version:
      logging.info(f"Chrome version: {version}")
    else:
      logging.warning("Failed to fetch Chrome version")
      logging.info("Script execution completed.")


chrome_version = get_chrome_version()
